# Technology comparison

**Owner:** Member B. **Status:** decisions for a later implementation. Nothing in this file is built in the 24 October repository.

Three decisions dominate the design. Each has three alternatives. The choice is tied to requirements in [06-requirements.md](06-requirements.md) and to limits recorded in [03-literature-review.md](03-literature-review.md).

## Decision 1 — How the battery schedule is computed

| Alternative | What it does | Fit to this project | Decision |
| --- | --- | --- | --- |
| Surplus rule | If PV exceeds load, charge up to power and state-of-charge limits. If load exceeds PV, discharge within the same limits. Otherwise idle | Easy to explain and fair as a baseline. No look-ahead, so it can fill the battery before a more useful interval and can cycle on small gaps. It cannot be the only method if the aim is to do better than current practice | **Baseline, not the proposed method.** Specified in [09-verification-plan.md](09-verification-plan.md) |
| Mixed-integer linear program (MILP), day-ahead | Binary variables stop simultaneous charge and discharge. Continuous variables set power and state of charge. The objective maximises on-site use of PV, with grid import and peak reported, and a throughput cap as a constraint | Same pattern as Talluri et al. and Sorour et al., who use MILP on forecasts and show that the objective changes the schedule [1], [2]. Constraints are checkable one by one. A 96-step day is a small problem for a laptop solver | **Chosen** |
| Reinforcement learning or a genetic search | A learned policy or a population search picks charge and discharge | Witharama et al. show a genetic algorithm plus forecasts can cut cost on a campus, with degradation in the objective [3]. The policy is hard to audit, needs more data than this team has, and can violate limits unless they are repaired afterwards. Reinforcement learning adds training instability without a site history to train on | **Rejected for the diploma** |

**Why MILP meets the requirements.** FR3 and FR4 require a schedule that respects power, state of charge, and a ban on simultaneous charge and discharge. A linear constraint set makes a violation either impossible or visible as an infeasible model. FR10 asks for a reason per interval; dual information or a direct reading of which constraint is tight can supply that reason. A learned policy cannot show the same proof. The surplus rule remains in the product so FR6 can be tested. It is not abandoned.

**Cost of the choice.** The model is only as good as linear efficiencies and a simplified throughput cap. A warranty curve that depends on temperature and depth of discharge will be approximated. That limitation is accepted and must be stated next to any result.

## Decision 2 — How PV and load are forecast

| Alternative | What it does | Fit to this project | Decision |
| --- | --- | --- | --- |
| Persistence | Tomorrow’s interval equals yesterday’s, or the last similar weekday, with PV forced to zero at night | Markovics and Mayer treat persistence as the skill baseline and still find large gains from better models on 15-minute PV data [4]. On an industrial load that repeats shifts, persistence can be strong. It ignores a weather forecast | **Required benchmark.** Not the forecast the scheduler trusts alone |
| Gradient boosting (LightGBM or an equivalent library) | Trees on lagged power, calendar features, and, for PV, weather-forecast irradiance and sun position | Witharama et al. use LightGBM for solar and building load before scheduling [3]. Training is practical on a year of 15-minute data. Feature importance gives the operator a partial explanation. Markovics and Mayer did not crown boosting; kernel methods and a neural net won on their PV plants [4]. Boosting is chosen as the default because it is strong, fast to retrain, and less brittle than an untuned deep model on a single site | **Chosen default** |
| Sequence neural model (LSTM or a small multilayer perceptron) | Learns temporal patterns from the raw series, optionally with weather inputs | Talluri et al. use a neural forecast in front of MILP [1]. Markovics and Mayer find a multilayer perceptron among the best PV models when it is tuned [4]. A sequence net needs more care against overfitting on one site and is harder to explain. It stays a permitted challenger in the evaluation plan if boosting does not beat persistence | **Challenger, not the default** |

**Why boosting plus a persistence score meets the requirements.** FR2 requires a day-ahead PV forecast and a day-ahead load forecast. The verification plan scores both with MAE and RMSE against persistence, which is the comparison Markovics and Mayer show is meaningful [4]. If boosting loses, the implementation must say so and may fall back to persistence inside the scheduler. Hiding a weak forecast would make the dispatch result uninterpretable.

**Cost of the choice.** Weather-forecast access may be missing for the study site. The model must still run with lags and calendar features only, and the report must name the missing input. A neural net is not forbidden later. It is not the commitment of this design.

## Decision 3 — What form the system takes

| Alternative | What it does | Fit to this project | Decision |
| --- | --- | --- | --- |
| Standalone decision-support model | A program reads tables (PV, load, tariff, battery limits), writes a schedule and a KPI comparison, and presents them in the operator views specified in [08-prototype.md](08-prototype.md). No live set-point | Matches the scope boundary: advice before any command. Can be tested on a file. Does not integrate vendor inverters | **Chosen** |
| Extend OpenEMS | Implement the scheduler as an OpenEMS energy-management controller on the existing device abstractions | OpenEMS already has meters, ESS channels, predictors, and a UI, and it is used on commercial sites [5]. The team would have to adopt Java OSGi component patterns and device drivers before the objective function is proven. That work does not help the 24 October question and is a poor use of the remaining diploma time unless a site standardises on OpenEMS | **Rejected as the core.** Allowed later as a deployment shell if a site requires it |
| Configure a vendor EMS (Schneider, Tesla commercial software, or a hybrid-inverter mode) | Turn on the supplier’s self-consumption or cost mode | [04-existing-systems.md](04-existing-systems.md) shows these products forecast and optimise, and that their formulations are not open. The team could not show why an interval changed, could not fix the objective to self-consumption, and could not publish the result without the vendor’s stack | **Rejected** |

**Why a standalone model meets the requirements.** NFR4 requires every schedule value to be traceable to a constraint. That is realistic if the team owns the model. NFR5 limits the system to one site, so a multi-tenant cloud EMS is unnecessary. FR1 is a file import, which a standalone tool can satisfy before any protocol work. OpenEMS remains the best host if the project ever sends set-points. Sending set-points is out of scope, so the host is out of scope too.

## Choices recorded for the README

| Decision | Choice |
| --- | --- |
| Dispatch | Day-ahead MILP, compared with the surplus rule |
| Forecast | Gradient boosting, scored against persistence; a neural model only as a challenger |
| Product form | Standalone decision-support model and the operator views in the prototype |

These choices assume A1–A8 in [02-relevance.md](02-relevance.md). If interviews show that the only acceptable system is the incumbent vendor controller, Decision 3 must be reopened and the scope rewritten. Until then the assumption stands, and it is labelled as an assumption.

## References

[1] G. Talluri, G. M. Lozito, F. Grasso, C. Iturrino Garcia, and A. Luchetta, “Optimal Battery Energy Storage System Scheduling within Renewable Energy Communities,” *Energies*, vol. 14, no. 24, art. 8480, 2021, doi: 10.3390/en14248480.

[2] A. Sorour, M. Fazeli, M. Monfared, A. A. Fahmy, J. R. Searle, and R. P. Lewis, “MILP Optimized Management of Domestic PV-Battery Using Two Days-Ahead Forecasts,” *IEEE Access*, 2022, doi: 10.1109/ACCESS.2022.3158303.

[3] W. M. N. Witharama, K. M. D. P. Bandara, M. I. Azeez, K. Bandara, V. Logeeshan, and C. Wanigasekara, “Advanced Genetic Algorithm for Optimal Microgrid Scheduling Considering Solar and Load Forecasting, Battery Degradation, and Demand Response Dynamics,” *IEEE Access*, 2024, doi: 10.1109/ACCESS.2024.3412914.

[4] D. Markovics and M. J. Mayer, “Comparison of machine learning methods for photovoltaic power forecasting based on numerical weather prediction,” *Renewable and Sustainable Energy Reviews*, vol. 161, art. 112364, 2022, doi: 10.1016/j.rser.2022.112364.

[5] OpenEMS contributors, “Edge Architecture,” https://openems.github.io/openems.io/openems/latest/edge/architecture.html, and https://github.com/OpenEMS/openems (accessed 12 October 2026).
