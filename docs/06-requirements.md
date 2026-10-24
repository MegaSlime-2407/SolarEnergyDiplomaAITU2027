# 6. Requirements

**Owner:** Musagali Kundyz.

Priorities are Must, Should, and Could. Every Must row has a check.

The four screens are the data-and-limits screen, the daily balance, the 24-hour plan, and the forecast error. The main calculation is the day-ahead optimization. The second calculation is the simple rule. Both use the same forecast.

## 6.1 Actors and objects

*Table 6.1. Actors and objects.*

| Name | Meaning |
| --- | --- |
| Energy specialist | Loads the file, reads the plan, and accepts or rejects it. |
| Engineer | Sets power, capacity, the charge window, the starting level, and the daily cycle limit. |
| Facility file | Solar panel power, load history, and an optional irradiance forecast. |
| Main plan | The optimized charge and discharge for 24 hourly intervals. |
| Simple rule | The baseline on the same forecast. It may exceed the daily cycle limit. |

## 6.2 Functional requirements

*Table 6.2. Functional requirements.*

| ID | Priority | Requirement | Acceptance |
| --- | --- | --- | --- |
| FR1 | Must | Accept one facility file and the battery limits: power, capacity, minimum and maximum state of charge, initial state of charge, and the daily cycle limit. Irradiance is optional. | A complete file is accepted. A file missing panel power, load, or the initial state of charge is rejected with the missing names. |
| FR2 | Must | Forecast solar generation and facility load for the next day in 24 hourly intervals, and also compute the same-as-yesterday forecast. | The output has 24 values for each series. No value is negative. |
| FR3 | Must | Produce the main plan for those 24 hours. The objective is solar energy used on site. Power, the state-of-charge window, and the daily cycle limit are hard constraints. The battery is not charged from the grid. Losses are not modelled. | An independent check replays state of charge. Equivalent cycles, charge plus discharge energy divided by twice the capacity, stay within the daily limit. |
| FR4 | Must | Run the simple rule on the same forecast. Solar covers the load first, surplus charges the battery, a deficit uses the battery down to the minimum, and the rest comes from the grid. | The rule is labelled simple rule. If it exceeds the daily cycle limit, the screen says so and does not hide the limit on the main plan. |
| FR5 | Must | Give every hour one reason, and name the limit when that limit stops a larger charge or discharge. | The 24-hour screen shows the reason. The solver said so is not a reason. |
| FR6 | Must | Report, for both calculations, the solar energy utilization rate, grid electricity consumption, unused surplus, and whether the battery limits hold. | Units are shown. A ratio is undefined when its denominator is zero. |
| FR7 | Must | When meter readings exist, show forecast against meter and the mean absolute error of both forecasts. | If the meters are absent, the forecast-error screen says so. It does not show a zero error. |
| FR8 | Must | Let the engineer edit the limits, including the daily cycle limit, and recompute both calculations. | A minimum above the maximum, a negative power, or a negative cycle limit is rejected. The previous and the new limits stay visible. |
| FR9 | Should | The specialist can accept or reject the plan. Rejection does not send a command to equipment. | The choice is stored. No set-point is written. |
| FR10 | Must | Offer the same plan through the web pages and, at the final milestone, through the Flutter application. | Both clients call the same API. The mobile application is not required for the first pre-defense screens. |
| FR11 | Must | Run the four scenarios: high solar generation, low solar generation, high facility demand, and limited battery capacity. | Each scenario names its file and reports FR6 for both calculations. |

## 6.3 Non-functional requirements

*Table 6.3. Non-functional requirements.*

| ID | Priority | Requirement | Acceptance |
| --- | --- | --- | --- |
| NFR1 | Must | A 24-hour plan, both forecasts, and both calculations finish in under 60 seconds on a laptop named in the test record. | The record states the machine and the elapsed time. |
| NFR2 | Must | Every Must requirement has a check. | Inspection of this table. |
| NFR3 | Must | The repository contains no passwords, API keys, or non-public meter files. | Inspection at each submission. |
| NFR4 | Must | The same file and limits produce the same plan. | Two runs match within 0.01 kW and 0.001 state of charge. |
| NFR5 | Must | One site and one battery. | The file has no second battery. |
| NFR6 | Must | The specialist can see the file check, the daily balance, the 24-hour plan with reasons, and the forecast error without opening a log. | The four screens in the prototype contain those fields. |
| NFR7 | Must | Charge and discharge losses stay out of the model. | The state-of-charge update uses efficiency 1, and the text says that losses are not modelled. |

## 6.4 Could, not commitments

*Table 6.4. Items that are not commitments.*

| ID | Statement | Why it is not a Must |
| --- | --- | --- |
| CO1 | A tariff or a cost column. | The proposal optimises solar used on site, not a bill. |
| CO2 | A deep learning forecast. | Section 5 does not choose it. |
| CO3 | A command to an inverter. | Out of scope in the proposal. |

## 6.5 Trace to the aim

*Table 6.5. Requirements traced to the proposal.*

| Aim | Requirements |
| --- | --- |
| Forecast the next day | FR2 and FR7. |
| Allocate the battery and respect the daily cycle limit | FR3, FR8, and NFR7. |
| Compare with the simple rule | FR4 and FR6. |
| Show a reason and let the specialist decide | FR5, FR9, and NFR6. |
| Web now, Flutter later, one API | FR10 and section 5. |
| Four scenarios and six indicators | FR6, FR7, FR11, and NFR6. |
