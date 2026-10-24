# 5. Technology comparison

**Owner:** Oralov Alinur.

The proposal, the interview, and section 10 fix the job the software has to do. It forecasts solar generation and facility load for the next day in 24 hourly intervals, then allocates the battery so that more solar energy stays at the facility. A simple rule runs on the same forecast and is the baseline. The specialist sees a reason for every hour and accepts or rejects the plan. The software does not control equipment.

Five decisions follow. The first two decide the calculation. The last three decide the stack already assigned in section 10: a backend and a database, web pages in HTML, CSS and JavaScript, a Flutter application, and deployment with Docker and nginx.

## 5.1 How the battery plan is calculated

*Table 5.1. The main calculation and the baseline are different calculations.*

| Alternative | What it does | Evidence | Decision |
| --- | --- | --- | --- |
| Linear optimization over the next 24 hours | Maximises solar energy used on site, subject to power, the state-of-charge window, and the daily cycle limit. Writes a reason for every hour. | Schneider documents model predictive control. ABB documents day-ahead optimisation. Gao et al. report 18.9% for greedy rules and 36.1% for a search method, on data that are not public. | Chosen as the main calculation |
| Simple rule on the same forecast | Solar covers the load first. Surplus charges the battery. A deficit uses the battery until the lower limit, then the grid. | This is the rule in the proposal. It is easy to check and can exceed the daily cycle limit. | Baseline. Not the main calculation |
| Reinforcement learning | An agent learns charge and discharge from a reward. | Gao et al., Jung et al., and Upadhyay et al. report savings in simulation. The hour cannot be traced to a published constraint. | Rejected |

The optimizer looks across the 24 hours and keeps the daily cycle limit. The simple rule does neither. The project will not claim the 36.1% or 9.2% cost figures from the papers. Charge and discharge losses are not modelled. The daily cycle limit stands in for wear.

## 5.2 How the next day is forecast

*Table 5.2. A forecast is required.*

| Alternative | What it does | Evidence | Decision |
| --- | --- | --- | --- |
| Gradient boosting, scored against same as yesterday | Lagged power, the hour, and irradiance when the file has it. Persistence is always computed beside it. | Section 10, steps 6 and 7. The literature review asks for the error of both forecasts. | Chosen |
| Same as yesterday only | Tomorrow’s hour repeats yesterday’s hour. | A required benchmark. The interview tied generation to the weather, so it is not enough alone. | Benchmark, computed beside the chosen forecast |
| A deep sequence model | An LSTM or a transformer predicts power or price. | Gao et al., Georgiadis et al., and Kanaan et al. use these models and also report large errors or data that are not industrial. | Not chosen |

*Note. The plan is not computed from the current hour alone.*

When meter readings for that day exist, both forecasts are scored with mean absolute error. That is the forecast-error screen.

## 5.3 Backend

*Table 5.3. Backend.*

| Alternative | What it does | Decision |
| --- | --- | --- |
| Python with FastAPI | One service runs the forecast, the optimizer, the simple rule, and the JSON API. The numerical libraries are Python libraries. | Chosen |
| Node.js | The API and the calculation live in JavaScript. The forecast and the solver would be a second stack. | Not chosen |
| Java with Spring | A compiled service exposes the API. Heavier than this diploma needs. | Not chosen |

*Note. Oralov Alinur owns this service.*

## 5.4 Database

*Table 5.4. Database.*

| Alternative | What it does | Decision |
| --- | --- | --- |
| PostgreSQL | Stores the facility file, the battery limits, both forecasts, and both 24-hour plans. | Chosen |
| SQLite | One file holds the same tables. Harder to share with a second process. | Not chosen |
| MongoDB | Documents instead of hourly rows. The plan is 24 rows with the same columns. | Not chosen |

## 5.5 How the screens reach the calculation

*Table 5.5. The web client remains HTML, CSS, and JavaScript.*

| Alternative | What it does | Decision |
| --- | --- | --- |
| REST JSON API behind nginx | The HTML pages and the Flutter application call the same endpoints. Docker Compose runs the API, PostgreSQL, and nginx. | Chosen |
| Clients read the database | Web and mobile connect to PostgreSQL. The calculation would be copied or skipped. | Rejected |
| GraphQL | One query language for both clients. The screens need a few fixed requests. | Not chosen |

*Note. The mobile client remains Flutter and Dart. Those choices are already fixed in the proposal and in section 10.*

## 5.6 Choices recorded for the project

*Table 5.6. No set-point is sent to an inverter.*

| Decision | Choice |
| --- | --- |
| Battery plan | Linear optimization for the next 24 hours. The simple rule is the baseline. |
| Forecast | Gradient boosting, with a same-as-yesterday forecast beside it. |
| Backend | Python and FastAPI. |
| Database | PostgreSQL. |
| Clients | HTML, CSS, and JavaScript, plus Flutter. Both use the REST API. Docker and nginx deploy the service. |
