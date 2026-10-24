# 4. Existing System Comparison

## 4.1 Selection of systems and comparison criteria

This section compares existing commercial energy management systems that coordinate on-site solar generation, battery storage, and grid supply, in order to show what is already available to an industrial facility and where the proposed system fits. Four systems were selected from vendors whose public documentation describes the control of PV and battery assets: Schneider Electric EcoStruxure Microgrid Advisor, Siemens Energy Load Optimization, ABB Ability OPTIMAX for Industrial Sites, and Higeco More Senergy EMS. Four systems fall within the required range of three to five. A system was included only if its capabilities could be confirmed from official vendor documentation; candidates that could not be confirmed in this way were left out.

The systems were compared using eight criteria that follow the data and decisions of the proposed project (solar generation, facility consumption, battery state of charge, grid availability, and the choice of the energy source at each moment):

- **C1. Target segment:** the type of site for which the system is intended.
- **C2. Input data:** the measurements and external data that the system uses.
- **C3. Forecasting:** whether generation and demand are predicted.
- **C4. Decision method:** rules, model predictive control, or other optimization.
- **C5. Battery management:** how charging and discharging are controlled and whether state of charge and aging are described.
- **C6. Grid and tariff interaction:** peak limiting, tariffs, export, and demand response.
- **C7. Operation mode and time horizon:** real-time control or planning ahead.
- **C8. Transparency and evidence:** whether the logic and the reported results are open and verifiable.

**Method and limits of the evidence.** All information comes from public vendor documentation retrieved in October 2026 (product pages, one product handout, and one vendor article), so the capabilities described are those claimed by the vendors. "Not specified" means that a function is not described in the sources reviewed; it does not prove that the function is absent. No system was tested hands-on.

## 4.2 Comparison table

Table 4.1 compares the four systems against the eight criteria. Each cell cites the vendor document on which it is based.

**Table 4.1.** Comparison of existing PV and battery energy management systems

| Criterion | Schneider Electric EcoStruxure Microgrid Advisor | Siemens Energy Load Optimization | ABB Ability OPTIMAX for Industrial Sites | Higeco More Senergy EMS |
| --- | --- | --- | --- | --- |
| **C1. Target segment** | Microgrids for commercial and industrial sites; one platform for solar, batteries, EV charging, generators, HVAC, and CHP (Schneider Electric, 2017, 2020). | Businesses and sites facing rising grid fees and volatile energy prices; controls loads, generators, and storage (Siemens, n.d.). | Industrial sites, microgrids, and smart cities (ABB, n.d.). | Renewable energy plants with battery storage (BESS); installed at the grid delivery point (Higeco More, n.d.). |
| **C2. Input data** | Real-time data from on-site distributed energy resources (DER) via a local edge controller (Modbus RTU, TCP/IP, BACnet, OpenADR 2.0); price signals, historical data, weather forecast, operating schedule (Schneider Electric, 2017, 2020). | Data from configured energy assets; the software optimizes consumption continuously in real time. List of measured variables not specified (Siemens, n.d.). | Site energy monitoring and reporting; weather and load forecasts; loads and prices (ABB, n.d.). | Network analyzer at the grid connection plus interfaces to inverters, batteries, and sensors; active and reactive power regulation (Higeco More, n.d.). |
| **C3. Forecasting** | Yes: supply and demand forecast from price signals, historical data, and weather forecast (Schneider Electric, 2020). | FLEX: forecasts loads and renewable generation. PDL (rule-based): not stated (Siemens, n.d.). | Yes: weather and load forecasts; basic machine learning and enhanced AI forecasting (ABB, n.d.). | Not specified in the sources reviewed (Higeco More, n.d.). |
| **C4. Decision method** | Model predictive control (MPC) in a cloud platform (Schneider Electric, 2020). | Two levels: PDL uses rule-based control with predefined constraints and priorities; FLEX uses predictive, AI-supported optimization (Siemens, n.d.). | Day-ahead optimization on forecasts, then real-time coordination; a learning system compensates deviations (ABB, n.d.). Algorithm not disclosed. | Selectable control strategies: peak shaving, band shaving, zero feed-in, self-consumption priority (Higeco More, n.d.). Optimization algorithm not described. |
| **C5. Battery management** | Charges the battery with excess solar, discharges at high prices, charges at negative prices (Schneider Electric, 2017, 2020). Battery aging and state-of-charge (SOC) limits not specified. | Storage regulated within predefined constraints and priorities (PDL) (Siemens, n.d.). Battery aging not specified. | Not explicitly described; energy assets are planned jointly to avoid peak loads (ABB, n.d.). | BESS stores PV surplus and covers plant consumption; phase balancing is stated to help battery lifespan (Higeco More, n.d.). |
| **C6. Grid and tariff interaction** | Tariff management (seasonal, day-ahead and hour-ahead), demand-charge avoidance, demand response (Schneider Electric, 2017). | Reduces peak demand and grid fees; FLEX reacts automatically to dynamic energy prices (Siemens, n.d.). | Peak-load avoidance; sale of surplus energy and participation in energy markets and demand response (ABB, n.d.). | Peak shaving against contractual power at the connection point; zero feed-in and zero injection limits (Higeco More, n.d.). |
| **C7. Operation mode and time horizon** | Real-time optimization; 48-hour default schedule if the server connection is lost (Schneider Electric, 2017, 2020). | Continuous real-time optimization (Siemens, n.d.). | Intra-day and day-ahead optimization with real-time correction (ABB, n.d.). | Real-time control; processing cycle up to 100 ms (Higeco More, n.d.). |
| **C8. Transparency and evidence** | Proprietary cloud platform; algorithm details not public. Reported case: bill reduction of about USD 500,000 per year at an Australian produce market (vendor-reported) (Schneider Electric, 2020). | Proprietary service delivered by Siemens (assessment, configuration, monitoring); no performance figures on the page (Siemens, n.d.). | Proprietary; up to 10% energy cost reduction claimed (vendor-reported, no method given) (ABB, n.d.). | Proprietary hardware panel, quote required; no performance figures (Higeco More, n.d.). |

*Source: compiled by the authors from vendor documentation (ABB, n.d.; Higeco More, n.d.; Schneider Electric, 2017, 2020; Siemens, n.d.), retrieved October 2026.*

## 4.3 Analysis of the comparison

All four systems manage solar generation, storage, and grid supply with the aim of lowering energy cost or limiting peak demand. They differ in how decisions are made. Schneider Electric, ABB, and the FLEX level of Siemens use forecasting and optimization (model predictive control or day-ahead and intra-day optimization), whereas the PDL level of Siemens and Higeco Senergy EMS rely on predefined rules and control strategies (ABB, n.d.; Higeco More, n.d.; Schneider Electric, 2020; Siemens, n.d.).

The comparison also shows what the public documentation does not contain:

- The logic used to choose between solar power, the battery, and the grid at each time step is not disclosed for any of the four systems; the sources describe goals and functions, not decision rules or algorithms (ABB, n.d.; Higeco More, n.d.; Schneider Electric, 2017, 2020; Siemens, n.d.).
- Battery state-of-charge limits and aging costs are not described, except for a statement by Higeco More that phase balancing helps battery lifespan (Higeco More, n.d.).
- The only quantitative results are vendor-reported: about USD 500,000 per year saved at one Australian market (Schneider Electric, 2020) and up to 10% energy cost reduction for OPTIMAX (ABB, n.d.). The documentation gives no test method or independent verification.

Independent research shows that the control method and the cost of the battery strongly affect results. In an industrial park, rule-based greedy control reduced cost by 18.9%, compared with 36.1% for a genetic algorithm and 35.9% for deep reinforcement learning (Gao et al., 2021). A model-based dispatch was 9.2% cheaper per day than a heuristic in another study (Kanaan et al., 2023). In a real food factory in Malaysia, a PV and battery system reduced electricity cost by 6.9%, and the authors name battery cost and the lack of financial incentives as barriers (Zahari et al., 2024). These findings suggest that transparent, well-defined decision logic and its validation on real measurements are important, and these are the aspects that vendor documentation leaves open.

## 4.4 Why the proposed solution is needed

The proposed system is a software-only decision-support tool for an industrial facility. From a facility file of solar power and facility load, it forecasts solar generation and load for the next day in 24 hourly intervals and recommends, for each interval, how to use solar energy: supply the facility directly, charge the battery with the surplus, discharge the battery, or import electricity from the grid. Every recommendation is given with a reason that the energy specialist can accept or reject, and the results are compared with a simple rule-based baseline.

The comparison supports the need for such a system in two respects. First, the commercial solutions reviewed are proprietary, and their decision logic, battery constraints, and performance evidence are not available in open documentation (criteria C4, C5, and C8). Second, they are delivered as vendor services, platforms, or hardware, and some require an assessment or a quotation before use (Higeco More, n.d.; Siemens, n.d.). For energy managers and engineers who need to understand, check, and adapt the decision rules, an open and explainable approach that works with basic measurements is therefore a justified goal.

This section does not claim that commercial systems perform worse than the proposed one, because the available evidence does not allow such a comparison. The contribution of the project is an explainable reference implementation whose decisions can be traced to the input measurements and evaluated on simulated or open data.

## References

ABB. (n.d.). *OPTIMAX® for industrial sites* [Product page]. Retrieved October 21, 2026, from [https://new.abb.com/process-automation/energy-industries/digital/solutions/abb-ability-energy-management-and-optimization-optimax/optimax-for-industrial-sites](https://new.abb.com/process-automation/energy-industries/digital/solutions/abb-ability-energy-management-and-optimization-optimax/optimax-for-industrial-sites)

Gao, Y., Li, J., & Hong, M. (2021). Machine learning based optimization model for energy management of energy storage system for large industrial park. *Processes, 9*(5), 825. [https://doi.org/10.3390/pr9050825](https://doi.org/10.3390/pr9050825)

Higeco More. (n.d.). *Senergy EMS – Energy management system* [Product page]. Retrieved October 21, 2026, from [https://higecomore.com/en/ems-energy-management-system/](https://higecomore.com/en/ems-energy-management-system/)

Kanaan, L., Ismail, L. S., Gowid, S., Meskin, N., & Massoud, A. M. (2023). Optimal energy dispatch engine for PV-DG-ESS hybrid power plants considering battery degradation and carbon emissions. *IEEE Access, 11*, 58506–58515. [https://doi.org/10.1109/ACCESS.2023.3281562](https://doi.org/10.1109/ACCESS.2023.3281562)

Schneider Electric. (2017). *EcoStruxure Microgrid Advisor* [Product handout]. Retrieved October 21, 2026, from [https://download.schneider-electric.com/doc/998-20080341_US/EcoStruxure%20Microgrid%20Advisor%20Handout.pdf](https://download.schneider-electric.com/doc/998-20080341_US/EcoStruxure%20Microgrid%20Advisor%20Handout.pdf)

Schneider Electric. (2020, November 12). *How AI powers today's advanced microgrids* [Article]. Schneider Electric Perspectives. Retrieved October 21, 2026, from [https://perspectives.se.com/blog-stream/how-ai-powers-today-s-advanced-microgrids](https://perspectives.se.com/blog-stream/how-ai-powers-today-s-advanced-microgrids)

Siemens. (n.d.). *Energy Load Optimization Service* [Product page, German version; English version at https://www.siemens.com/en-us/content/energy-load-optimization-service/]. Retrieved October 21, 2026, from [https://www.siemens.com/de-de/content/energy-load-optimization-service/](https://www.siemens.com/de-de/content/energy-load-optimization-service/)

Zahari, N. E. M., Mokhlis, H., Mubarak, H., Mansor, N. N., Sulaima, M. F., Ramasamy, A. K., Zulkapli, M. F., Ja'apar, M. A. B., Jaafar, M., & Marsadek, M. B. (2024). Integrating solar PV, battery storage, and demand response for industrial peak shaving: A systematic review on strategy, challenges and case study in Malaysian food manufacturing. *IEEE Access, 12*, 106832–106856. [https://doi.org/10.1109/ACCESS.2024.3420941](https://doi.org/10.1109/ACCESS.2024.3420941)
