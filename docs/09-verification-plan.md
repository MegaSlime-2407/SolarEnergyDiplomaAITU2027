# 9. Verification and evaluation

**Owner:** Oralov Alinur.

This is a plan only. No plan has been optimised by software, and no saving is claimed.

The six indicators and the four scenarios are the ones in the proposal. The baseline is the simple rule, not an idle battery.

## 9.1 What is compared

*Table 9.1. Both arms use the same file, the same limits, and the same forecast.*

| Arm | Definition |
| --- | --- |
| Main | The 24-hour linear optimization, using the gradient-boosted forecast, checked by replaying state of charge and the daily cycle limit. |
| Baseline | The simple rule on the same forecast. Solar covers the load first. Surplus charges the battery. A deficit uses the battery down to the minimum, then the grid. The rule does not reduce power to save cycles. |

*Note. Losses are not modelled.*

Equivalent cycles equal charge energy plus discharge energy, divided by twice the nominal capacity.

## 9.2 Indicators

*Table 9.2. The six indicators from the proposal.*

| Indicator | What the record contains |
| --- | --- |
| Solar energy utilization rate | Solar energy that served the load or charged the battery, divided by solar energy. |
| Grid electricity consumption | Kilowatt-hours imported in the scenario. |
| Surplus solar energy | Solar energy that was neither used on site nor stored. |
| Algorithm correctness | Pass or fail against power, the state-of-charge window, no charging from the grid, and the daily cycle limit. |
| System usability | Whether the four screens show the file check, the balance, the hourly reason, and the forecast error. |
| Forecast error | Mean absolute error of both forecasts when meters exist. Otherwise the screen says the meters are absent. |

*Note. Paper percentages and vendor percentages are not targets.*

## 9.3 Hand-checked fixture

Four hours stand in for the arithmetic. The implemented horizon is still 24 hours. Capacity 10 kWh, state of charge from 0.20 to 0.90, start 0.50, power limit 4 kW, daily cycle limit 0.40. That limit allows 8 kWh of charge plus discharge. Photovoltaic power is 6, 1, 6, 0 kW. Load is 2, 5, 2, 3 kW. This fixture uses the powers directly, so it checks the allocation rather than a forecast.

Main plan: charge 4 kW, discharge 2 kW, charge 2 kW, then hold. The discharge and the second charge are limited by the daily cycle limit. Hour 4 imports from the grid because the cycle allowance is used up.

*Table 9.3. Fixture.*

| Check | Main plan | Simple rule |
| --- | --- | --- |
| State of charge | 0.50, 0.90, 0.70, 0.90, 0.90 | 0.50, 0.90, 0.50, 0.90, 0.60 |
| Powers, charge then discharge (kW) | (4, 0), (0, 2), (2, 0), (0, 0) | (4, 0), (0, 4), (4, 0), (0, 3) |
| Inside 0.20–0.90 and 4 kW | Yes | Yes |
| Throughput | 8 kWh, 0.40 cycles | 15 kWh, 0.75 cycles |
| Daily cycle limit | Held | Exceeded. The screen must say so. |
| Solar used on site | 11 of 13 kWh | 13 of 13 kWh |
| Grid import | 5 kWh, peak 3 kW | 0 kWh |
| Unused surplus | 2 kWh | 0 kWh |

*Note. The simple rule uses more solar by cycling past the limit. That ratio is not a successful arm.*

An implementation that disagrees with this table fails the check. The table is not a factory result.

## 9.4 Scenarios and data

*Table 9.4. Data conditions.*

| Condition | Rule |
| --- | --- |
| Scenarios | High solar generation, low solar generation, high facility demand, and limited battery capacity. Each is a named file. |
| Step | 24 hourly intervals. The proposal states the one-hour step as an assumption, and the screens use that step. |
| Site | One industrial facility, named only with permission. Simulated or open data are allowed and must be labelled. |
| Battery | Limits, including the daily cycle limit, are inputs. They are not tuned after the score. |
| Losses | Not modelled. |
| Substitute series | Allowed only with a citation and a mismatch statement. The Pecan Street series is residential. |

## 9.5 Pass and fail

1. The fixture table is reproduced within 0.01 kW and 0.001 state of charge.
2. On each scenario, the main plan meets the limits or the failing hours are listed.
3. The simple rule is reported on the same forecast, including a cycle-limit warning when it applies.
4. The six indicators are the ones in this section. Usability refers to the four screens. Forecast error is reported or marked absent.
5. The prose does not say that the system beat EcoStruxure, Siemens, OPTIMAX, Senergy, or any percentage in the literature review.

A feasible main plan with a lower utilization than a simple rule that broke the cycle limit is a valid result. It must be reported. It is not a reason to drop the cycle limit after the run.
