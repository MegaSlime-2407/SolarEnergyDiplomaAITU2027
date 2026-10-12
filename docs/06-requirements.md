# Requirements specification

**Owner:** Member C. **Status:** initial requirements for the 24 October pre-defense. Mandatory items are written so a later test or an inspection can fail them. Priorities are Must, Should, and Could.

Identifiers are stable. [05-technology-comparison.md](05-technology-comparison.md) and [09-verification-plan.md](09-verification-plan.md) refer to these numbers.

## Actors and objects

| Name | Meaning |
| --- | --- |
| Energy manager | Reviews forecasts, the schedule, and KPI comparisons |
| Maintenance engineer | Edits battery limits |
| Study file | 15-minute time series and scalar battery and tariff parameters for one site and one horizon |
| Schedule | For each interval: charge power, discharge power, state of charge, grid import, and a reason code |
| Surplus rule | The baseline defined in [09-verification-plan.md](09-verification-plan.md) |

## Functional requirements

| ID | Priority | Statement | Acceptance criterion | How to check |
| --- | --- | --- | --- | --- |
| FR1 | Must | The system accepts one site’s study file: timestamped PV power, site load, initial state of charge, battery energy capacity, charge and discharge power limits, minimum and maximum state of charge, charge and discharge efficiency, a daily throughput cap, and optional import and export prices | A file that matches the column list in [08-prototype.md](08-prototype.md) is accepted. A file missing PV power, load, or initial state of charge is rejected with the name of each missing field. Units are kW, kWh, and 0–1 for state of charge and efficiency | Later: fixture files, one valid and one invalid. Now: the column list exists in the prototype |
| FR2 | Must | Given history and, when present, a weather forecast, the system produces a PV power forecast and a load forecast for each interval of the next day | For a day with 96 intervals, both forecasts have 96 values, PV is zero when the solar elevation is below zero if that elevation is provided, and neither forecast contains negative power. Error against metered values is reported with MAE and RMSE, including the same scores for persistence | Later: forecast unit test on a withheld day. Now: FR2 names the scores the evaluation plan must compute |
| FR3 | Must | The system produces a battery schedule for every interval in the horizon | The output table has one row per input interval and no missing power or state-of-charge cell | Later: row-count assertion. Now: the output columns are listed in the prototype |
| FR4 | Must | The schedule respects charge and discharge power limits, state-of-charge bounds, efficiency, the daily throughput cap, a ban on simultaneous charge and discharge, a ban on charging from the grid, and a ban on exporting battery energy | For every row, charge and discharge are each within \[0, Pmax\], at most one of them is positive, charge energy does not exceed PV surplus after the load, discharge energy does not exceed the load that PV did not cover, state of charge stays inside \[SOCmin, SOCmax\], the state-of-charge update matches power, step length, and efficiency within a stated numeric tolerance, and charge energy plus discharge energy does not exceed the daily throughput cap | Later: constraint checker on the solver output, independent of the solver’s own claim. Now: the constraint list is the one in this row |
| FR5 | Must | The system reports self-consumption rate, self-sufficiency, grid-import energy, peak grid-import power, and battery throughput for the horizon | Each indicator uses the formula in [09-verification-plan.md](09-verification-plan.md). Units are shown. Division by zero (no PV, or no load) is reported as “undefined”, not as zero | Later: hand-calculated fixture of four intervals. Now: formulas exist in the verification plan |
| FR6 | Must | The system runs the surplus rule on the same forecasts or the same metered series, as selected by the user, and reports FR5’s indicators for both | Both KPI blocks are present, the baseline block is labelled “surplus rule”, and the energy balance of the baseline also satisfies FR4 except the throughput cap. The surplus rule may be infeasible with respect to the throughput cap; if so, the report says so and does not silently drop the cap for the proposed schedule | Later: paired KPI fixture. Now: the rule is specified in the verification plan |
| FR7 | Should | When metered PV and load exist for the horizon, the system shows forecast versus meter | A plot or table aligns forecast and meter on the same timestamps, and MAE and RMSE from FR2 are visible without opening a log file | Later: UI or report inspection on a day that has actuals |
| FR8 | Must | The maintenance engineer can change power limits, state-of-charge bounds, initial state of charge, and the throughput cap, then recompute | After a change, FR3–FR6 are produced from the new limits. The previous limits and the new limits are both visible. A limit with SOCmin greater than SOCmax, or a negative power limit, is rejected | Later: edit-and-recompute test. Now: the battery screen in the prototype lists these fields |
| FR9 | Should | The energy manager can export the schedule as a table | The export contains the columns in the prototype’s schedule screen and opens in a spreadsheet without manual splitting | Later: export a CSV and open it |
| FR10 | Should | Each interval carries a plain-language reason: charge from surplus, discharge to cover load, hold for a later interval, or idle at a limit | Every row has exactly one reason code from that set. For a fixture where the throughput cap binds, at least one row is “idle at a limit” or “hold for a later interval”, and the report names the cap | Later: fixture with a tight throughput cap. The MILP choice in the technology comparison is what makes this check possible |

## Non-functional requirements

| ID | Priority | Statement | Acceptance criterion | How to check |
| --- | --- | --- | --- | --- |
| NFR1 | Must | A 96-interval horizon completes forecasts, both schedules, and the KPI block in under 60 seconds on a laptop the team names in the test record | The test record states the machine, the solver, and the elapsed time. The time is under 60 seconds. A longer run fails this requirement even if the schedule is feasible | Later: one timed run. Not applicable to this documentation tag |
| NFR2 | Must | Every Must requirement in this file has a check that a reviewer can apply | This table has a non-empty “How to check” cell for every Must row. A Must row with only “to be defined” fails | Inspection of this document |
| NFR3 | Must | The repository contains no passwords, API keys, personal meter files, or contact details that are not already public | A review of the tree finds no `.env` secrets and no private interview data. Public company emails in [interviews/contacts.md](interviews/contacts.md) are allowed because they are published by those organisations | Inspection at each pre-defense tag |
| NFR4 | Must | A reviewer can trace a scheduled power back to the constraint that shaped it | For any sampled interval, the output shows the power, the state of charge, the active reason code (FR10), and, when a bound is tight, the name of that bound. “The solver said so” is not an acceptable trace | Later: sample three intervals from a solved day, including one at a bound |
| NFR5 | Must | The system is specified for one site and one battery | The study file has no site-identifier column that changes behaviour, and the architecture has no portfolio optimiser. A request to schedule two batteries is out of scope, not a hidden feature | Inspection of the study-file columns and [07-architecture.md](07-architecture.md) |
| NFR6 | Must | Text that depends on practitioners distinguishes verified findings from assumptions | [02-relevance.md](02-relevance.md) keeps a verified section that is empty until the log says otherwise. A design document that says “interviews showed” without a log ID fails | Inspection of the relevance note and the interview log |
| NFR7 | Must | The same study file, limits, and forecast inputs produce the same schedule | Two consecutive runs write identical schedule tables, allowing a documented numeric tolerance not larger than 0.01 kW and 0.001 state of charge | Later: diff two runs. A stochastic solver would fail unless it is pinned |

## Could, recorded so they are not mistaken for commitments

| ID | Statement | Why it is not a Must |
| --- | --- | --- |
| CO1 | Intraday correction of the day-ahead schedule when live meters diverge from the forecast | Talluri et al. do this. It is a later extension. The first evaluation uses the day-ahead schedule only |
| CO2 | A neural-network forecast challenger | Allowed by the technology comparison if boosting loses to persistence. Not required for acceptance |
| CO3 | Hosting the scheduler inside OpenEMS | Deployment option only. The core remains the standalone model |

## Trace to the aim

| Aim fragment | Requirements |
| --- | --- |
| More of the site’s PV used on site | FR5, FR6, and the primary term in the objective described in the architecture |
| Without breaking battery limits | FR4, FR8, NFR4 |
| Compared with a surplus rule | FR6 |
| One industrial facility | FR1, NFR5 |
| Explainable to an energy manager | FR7, FR9, FR10, NFR4 |

## Open points that are assumptions

Until [02-relevance.md](02-relevance.md) records a verified finding, FR5’s choice to rank self-consumption above peak demand is assumption A6, and the presence of prices in FR1 as optional fields is assumption A7. If interviews reverse that ranking, FR5 stays, and the objective priority in the architecture is edited in the same change.
