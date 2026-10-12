# Architecture

**Owner:** Member C. **Status:** description aligned with the 24 October diagrams. Components are a draft. They are not deployed services.

The system is a decision-support tool, called here the Dispatch Advisor, for one grid-connected industrial site. It reads a study file and writes a day-ahead battery schedule plus a comparison with the surplus rule. It does not connect to inverters.

Diagrams, with editable Mermaid sources and SVG exports:

| View | Source | Export |
| --- | --- | --- |
| System context | [../diagrams/context.mmd](../diagrams/context.mmd) | [../diagrams/exports/context.svg](../diagrams/exports/context.svg) |
| Use cases | [../diagrams/use-case.mmd](../diagrams/use-case.mmd) | [../diagrams/exports/use-case.svg](../diagrams/exports/use-case.svg) |
| Components (draft) | [../diagrams/component.mmd](../diagrams/component.mmd) | [../diagrams/exports/component.svg](../diagrams/exports/component.svg) |

## Context

External to the software:

- **Energy manager** — asks for a schedule and reads KPIs. Primary actor (assumption A1).
- **Maintenance engineer** — supplies battery limits (FR8).
- **Meter archive** — historical and, when available, same-day PV power, site load, and battery state of charge. In this stage the archive is a file, not a live SCADA link.
- **Weather forecast** — optional irradiance and related fields for the PV model (FR2).
- **Tariff table** — optional import and export prices (FR1). Missing prices do not block a schedule. They block only a cost column.

The Dispatch Advisor is the single system in the context diagram. The battery, the PV array, and the grid are physical equipment represented by numbers in the study file. They are not software actors. Drawing them as devices to be commanded would contradict the scope.

## Use cases

| ID | Name | Actor | Requirements |
| --- | --- | --- | --- |
| UC1 | View site energy balance | Energy manager | FR5, and the overview screen |
| UC2 | Set battery limits | Maintenance engineer | FR8, FR4 |
| UC3 | Generate day-ahead schedule | Energy manager | FR1, FR2, FR3, FR4, FR10 |
| UC4 | Compare with the surplus rule | Energy manager | FR6, FR5 |
| UC5 | Inspect forecast error | Energy manager | FR2, FR7 |

UC3 includes forecasting. The include is inside the Dispatch Advisor, not a separate actor. UC4 uses the same horizon as UC3. UC5 is available only when metered values exist; otherwise the screen states that they are absent (FR7).

## Draft components

| Component | Responsibility | Does not do |
| --- | --- | --- |
| Operator views | The five screens in [08-prototype.md](08-prototype.md). Collect the study file and the limit edits. Show schedules and KPIs | Solve the schedule |
| Data intake | Parse and validate the study file (FR1). Reject illegal limits (FR8) | Fill missing PV by guessing |
| PV forecast | Day-ahead PV power (FR2). Default model class is gradient boosting. Always computes the persistence forecast as well | Call a weather service of its own design. It consumes a weather series if one is in the file |
| Load forecast | Day-ahead site load (FR2), same rule on persistence | Shift or curtail the load |
| Optimizer | Build the day-ahead MILP and return charge, discharge, and state of charge (FR3, FR4) | Talk to hardware |
| Baseline scheduler | Apply the surplus rule to the same series the user selected (FR6) | Share variables with the MILP. It is a separate calculation so a bug in one does not define the other |
| Constraint checker | Recompute state of charge from the published powers and flag any FR4 breach. This check is outside the solver | Repair a broken schedule silently |
| KPI reporter | Apply the formulas for both schedules (FR5) and attach reason codes where the checker or the solver marks a tight bound (FR10, NFR4) | Rank the two schedules as “better” if self-consumption is undefined |

Data moves in one direction during a run: operator views → data intake → forecasts → optimizer and baseline scheduler, in parallel → constraint checker → KPI reporter → operator views. The checker reads both schedules. Forecasts also go to the reporter so UC5 can be drawn without a second pipeline.

## Objective inside the optimizer

For each interval \(t\) of length \(\Delta t\):

- \(P^{pv}_t\), \(P^{load}_t\): forecast power, kW.
- \(P^{ch}_t\), \(P^{dis}_t\): charge and discharge, kW, each \(\ge 0\).
- At most one of \(P^{ch}_t\) and \(P^{dis}_t\) is positive.
- State of charge \(E_t\) in kWh updates with charge efficiency and discharge efficiency.
- \(E_t\) stays inside the engineer’s window.
- Sum of \(P^{ch}_t \Delta t + P^{dis}_t \Delta t\) over the day stays within the throughput cap.
- Charge energy does not exceed PV surplus after the on-site load, so the battery is not charged from the grid.
- Discharge energy does not exceed the part of the load that PV did not cover, so the battery is not exported.
- On-site solar use in an interval is the PV energy that serves the load directly plus the PV energy that charges the battery.
- Grid import covers load that is not served by PV or by discharge.

The objective maximises total on-site solar use over the horizon. Grid-import energy and peak import are computed after the solve and shown beside the surplus rule. They are not the objective, because [03-literature-review.md](03-literature-review.md) shows cost and self-consumption diverging. Putting peak into the objective would be a change of aim and requires a revision of assumption A6, not a silent extra term.

If the model is infeasible, the operator view says infeasible and names the conflicting limits. It does not return the surplus-rule schedule under the MILP’s name.

## Why the draft is consistent

| Concern | Where it is closed |
| --- | --- |
| Requirements name behaviour the components must provide | FR1–FR10 map onto the table above |
| The context has the same actors as the use-case diagram | Energy manager and maintenance engineer only |
| No component issues a set-point | Stated on the optimizer row and in the context section |
| The baseline cannot be “optimised away” | Baseline scheduler is a separate component |
| One site | Data intake accepts one study file (NFR5) |

## Deferred structure

An intraday corrector (CO1) would sit between the checker and the views and would read live meters. It is not in the component diagram. An OpenEMS adapter (CO3) would sit outside data intake. It is not in the diagram. Adding either box without a requirement change would make the draft inconsistent with the scope.
