# 8. UX / prototype

## User Interaction and Interface Mockups

The proposed system is a web-based decision-support platform intended for the energy specialist of an industrial facility, with an adapted mobile interface for reviewing and accepting the plan away from the workstation. In both versions, interaction with the system is organized around four screens. Mockups of the web version are provided below (Figures 8.1–8.4), and mockups of the mobile version follow them (Figures 8.5–8.6). The key user scenarios are described below.

### Scenario 1. Configuration of battery limits and loading of facility data

The specialist defines the operating limits of the battery storage system once: rated power, capacity, permissible state-of-charge range, initial charge level, and the maximum number of equivalent cycles per day. Subsequently, a facility data file is uploaded, containing the installed solar panel power, the historical load profile, and, optionally, a solar irradiance forecast. A validation step precedes any calculation: if the panel power, the load data, or the initial charge level is missing, the calculation is blocked and the system reports the missing item (Figures 8.1 and 8.5(a)).

### Scenario 2. Analysis of the daily energy balance

For the following day, the system presents the distribution of solar energy among direct consumption, battery charging, and unused surplus, together with grid consumption and battery cycle usage. If the baseline rule-based strategy would exceed the permitted cycle limit, the interface displays an explicit warning (Figures 8.2 and 8.5(b)).

### Scenario 3. Examination of the hourly plan

The plan covers 24 hourly intervals. For each interval, the specialist can review the battery charge or discharge power, the resulting state of charge, the power drawn from the grid, and a brief justification of the decision. The specialist may switch between the main optimized calculation and the simple rule-based strategy, both computed on identical input data. The system provides recommendations only; the specialist accepts or rejects the proposed plan, and no control commands are issued to the equipment (Figures 8.3 and 8.6(a)).

### Scenario 4. Assessment of forecast accuracy

When meter readings are available, the system compares forecast and actual solar generation and reports the mean absolute error, allowing the specialist to judge the reliability of the forecast (Figures 8.4 and 8.6(b)).

Input and output data. The input consists of (i) a facility data file (solar panel power, hourly load history, optional irradiance forecast) and (ii) battery limits specified by the specialist. The output consists of (i) a 24-hour plan (battery power, state of charge, grid power, and justification for each interval) and (ii) daily summary indicators (share of solar energy utilized, number of battery cycles, grid energy consumed).

Web version. The web version is intended for work at the specialist’s workstation. It uses a full-width layout with a side navigation menu and presents the hourly plan as a single table with all indicators in one view.

*Figure 8.1. Mockup of the "Data and limits" screen of the web version (battery limits, facility file and test scenarios, file check).*

*Figure 8.2. Mockup of the "Daily balance" screen of the web version (use of solar energy, daily summary and battery plan).*

*Figure 8.3. Mockup of the "24-hour plan" screen of the web version (hourly plan with a reason for every interval).*

*Figure 8.4. Mockup of the "Forecast error" screen of the web version (forecast against meter readings).*

Mobile version. The mobile interface reproduces the same four screens and the same calculation, so that every scenario described above can be carried out from a phone. Navigation is moved to a bottom bar, and the principal actions (calculation of the plan, acceptance or rejection of the plan) are fixed at the bottom of the screen. The wide hourly table is replaced by a list of cards, each presenting the hour, the justification of the decision, the state of charge, the grid power, and the battery power. The mobile interface belongs to the same recommendation-only platform and introduces no additional functions.

*Figure 8.5. Mockups of the mobile version: (a) the "Data and limits" screen; (b) the "Daily balance" screen.*

*Figure 8.6. Mockups of the mobile version: (a) the "24-hour plan" screen; (b) the "Forecast error" screen.*

Interaction with external systems. The only external input is the facility file uploaded by the specialist. The system has no connection to inverters or battery controllers. The web pages and, at the final milestone, the mobile application call the same REST JSON API, which validates the file, runs both calculations, and returns the plan. The decision of the specialist to accept or reject the plan is stored, and no set-point is written to equipment.

Examples of input and output data. Table 8.1 shows the input for the typical test day, and Table 8.2 shows an excerpt of the resulting 24-hour plan. In Table 8.2, a positive battery power is charging and a negative one is discharging.

**Table 8.1. Example of input data.**

| Input | Example |
| --- | --- |
| Facility file | Installed solar panel power, 140 kW; hourly load history in kW; optional hourly irradiance forecast for the next day |
| Battery limits | Power 40 kW; capacity 100 kWh; charge range 20–95%; initial charge 60%; cycle limit 1.0 per day |

**Table 8.2. Example of output data: an excerpt of the 24-hour plan for the typical test day.**

| Hour | Solar, kW | Load, kW | Battery, kW | Charge, % | Grid, kW | Reason |
| --- | --- | --- | --- | --- | --- | --- |
| 08:00–09:00 | 34.3 | 54.5 | −20.2 | 23 | 0.0 | Battery covers the deficit |
| 12:00–13:00 | 80.6 | 54.0 | +26.5 | 47 | 0.0 | Surplus goes to the battery |
| 22:00–23:00 | 0.0 | 32.3 | −32.2 | 63 | 0.1 | Battery covers the deficit |
