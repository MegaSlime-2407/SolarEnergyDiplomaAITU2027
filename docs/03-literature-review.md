# 3. Literature Review

## 3.1 Scope and selection of sources

This review examines twelve sources: ten peer-reviewed publications (eight research articles, one systematic review with a case study, and one analytical review) and two reports of international energy agencies. The sources were identified through keyword searches in academic databases (IEEE Xplore and Scopus) that combined the terms energy management, photovoltaic, battery storage, industrial, forecasting, reinforcement learning, and battery degradation. A source was retained when it addresses the coordination of PV generation, electrical load, and battery storage; when it is set in an industrial facility or a comparable system, or documents a method that can be transferred to one; and when it reports quantitative results.

Because the field develops quickly, the core of the review consists of publications from 2022 to 2025, which account for ten of the twelve sources. Two papers from 2021 (Gao et al., 2021; Kermani et al., 2021) are retained as reference points for rule-based and early machine-learning dispatch. The two institutional reports (IEA, 2024; IRENA, 2025) provide the economic context rather than evidence about control methods. The review addresses three questions: which approaches exist, what is already known, and which limitations the project takes into account.

## 3.2 Structured analysis of the publications

Table 3.1 summarizes each source by problem context, method, data, main findings, and limitations. Percentages are quoted as reported by the authors. They are not directly comparable between studies, because the reference cases, system sizes, and tariffs differ.

**Table 3.1.** Structured analysis of the reviewed sources

| Source | Context and problem | Method / technology | Data | Main findings | Limitations |
| --- | --- | --- | --- | --- | --- |
| **Kermani et al. (2021)** | University building microgrid (12 kW PV, 6.5 kWh battery); reduce grid import. | Rule-based priority control of three load classes in a SCADA system; Simulink model. | 2019 measurements of a laboratory microgrid; tariff 0.25 EUR/kWh. | Monthly cost reduction of about 57% (PV only) and about 88% (PV and battery); payback about seven years. | Laboratory scale; no forecasting; numerical inconsistencies within the paper. |
| **Gao et al. (2021)** | Industrial park with PV buying on the spot market; dispatch plan and battery size. | GAN-LSTM PV forecast; simple-average load forecast; greedy, genetic algorithm (GA) and DDPG dispatch. | Hourly PV and load data of a real park (not public); spot prices. | Cost reduced by 18.9% (greedy), 36.1% (GA), 35.9% (DDPG); storage pays off only below about 318.85 RMB/kWh. | Daily optimization only; battery charged from PV only; large PV forecast error; tied to the Chinese market. |
| **Amini et al. (2023)** | PV farm with a 500 kWh battery in an electricity market; battery aging ignored in schedules. | MPC-style MILP with linearized calendar and cycle aging cost; MLP price forecast. | Historical PV and price data of the Illinois Institute of Technology microgrid; simulation. | Against a simple controller: capacity fade −5.06%, degradation cost −4.67%, profit +1.10% (abstract values). | Simulation only; PV farm, not an industrial facility; aging linearized. |
| **Kanaan et al. (2023)** | Hybrid PV-diesel-battery plant; dispatch with aging and carbon cost. | LSTM forecasts and MILP dispatch re-solved every 15 minutes with feedback; SOC and state-of-health limits. | Pecan Street data of 75 US homes (2018), reduced to 15 minutes; simulated 80 kW PV, 100 kWh battery, 100 kW diesel. | Daily cost 9.2% below a heuristic and 3.5% below a stochastic method; emission cost 29.4% lower. | Residential data; simulated plant with diesel; one-day evaluation; no investment analysis. |
| **Benavides et al. (2022)** | Fluctuating PV, wind and hydrokinetic sources with an industrial load; grid stability. | Laboratory tests of ramp-rate and moving-average power smoothing with supercapacitor and lithium-ion storage. | Measured renewable profiles and laboratory microgrid hardware; industrial load profile. | Ramp-rate method makes the supercapacitor work fewer cycles; the result holds when source capacity changes. | Power quality, not energy cost; laboratory scale; non-solar sources; no tariff optimization. |
| **Miah et al. (2022)** | Storage controllers and optimization schemes in microgrids. | Analytical review of 110 highly cited Scopus papers (2010–2021); 24 controllers and 21 optimization schemes compared. | 110 papers. | Compares controllers and optimization schemes and identifies limitations and research gaps in the selected papers. | Coverage ends in 2021; microgrids in general, not industry; no own experiments. |
| **Upadhyay et al. (2024)** | Industrial microgrid in Norway (200 kWp PV, 1.1 MWh battery); cost under hourly and peak pricing. | PPO and TD3 reinforcement learning with random-forest load forecast against a threshold-based logic benchmark. | Hourly data of a real site, February–July 2024; PV profile modeled; Nord Pool prices. | About 20% more monthly saving than the logic benchmark; TD3 cut peaks more strongly under peak pricing. | Six months only; very long training (50 million steps); scalability untested; PV modeled. |
| **Zahari et al. (2024)** | Industrial peak shaving with PV, battery and demand response. | Systematic review of 55 papers (2018–2022) and a threshold-based case study in a food factory. | Real factory in Malaysia, readings every 5 s, one month (about 66 MWh). | Battery supplied 839 kWh; energy cost −6.9%, CO2 −8.6%; framework proposed. | Small, non-optimized system; one month; review ends in 2022. |
| **Jung et al. (2025)** | Industrial building (250 kW PV, 1000 kWh storage); cost, peak and battery wear together. | Two PPO agents (cost and switching) combined by Pareto selection (MAPPO); compared with PPO, TD3, SAC. | Real industrial building load (one year, 15-minute steps); PV modeled from irradiance; time-of-use tariff. | Cost −14.68% against no storage; 35.2% fewer switching events than PPO. | Simulation; five-day test period; no export to the grid; battery size not optimized. |
| **Georgiadis et al. (2025)** | Manufacturing plant with 2 MW PV in Greece; volatile prices; battery operation and investment. | Transformer and MLP forecasts; 24-hour hourly MILP; investment analysis with aging and subsidy. | Plant data (PV Jan 2023–May 2024; load three months); prices 2020–2023; four representative days. | A 1 MW / 2 MWh battery cut daily cost by up to 352 RMU; payback about seven years, shorter with a subsidy. | Four days only; hourly steps; PV forecast weak in sudden weather change; simplified aging; data on request. |
| **IEA (2024)** | Role of batteries in secure energy transitions (global). | Scenario-based assessment of demand, supply, costs and policy. | Global energy-sector data and scenarios. | Storage must grow about sixfold by 2030; behind-the-meter use becomes more attractive as costs fall. | Global scenarios; no site-specific operating schedule. |
| **IRENA (2025)** | Cost of renewable power generation in 2024 (global). | Cost review: LCOE, installed cost, capacity factor, storage cost. | Global project data for 2024. | Solar PV LCOE USD 0.043/kWh; utility-scale battery cost USD 192/kWh, 93% below 2010. | Global, utility-scale averages; may not match a local facility. |

*Note. RMU = relative monetary units, the anonymized currency used by Georgiadis et al. (2025). Source: compiled by the authors from the cited publications.*

## 3.3 Approaches in the literature

### 3.3.1 Economic and technical context

The International Energy Agency (IEA, 2024) identifies batteries as central to the integration of variable renewable energy and estimates that energy storage capacity must grow about sixfold by 2030 to meet global climate goals. It also notes that batteries become more attractive for utility-scale and behind-the-meter use as costs fall. The International Renewable Energy Agency (IRENA, 2025) reports that new solar PV generated electricity at a global weighted-average cost of USD 0.043/kWh in 2024 and that the cost of utility-scale battery storage fell by 93% since 2010, to USD 192/kWh. Together, the two reports indicate that the economic case for combining PV with storage is strengthening. Both, however, describe global or utility-scale averages and do not specify how an individual facility should operate its battery from interval to interval, which is the question addressed by the studies reviewed below.

### 3.3.2 Rule-based and threshold control

The simplest approach allocates energy by fixed priority or threshold rules. Kermani et al. (2021) implemented such rules in a SCADA-supervised laboratory microgrid with a 12 kW PV array and a 6.5 kWh battery serving three load classes, and reported monthly cost reductions of about 57% with PV alone and about 88% with PV and battery. Zahari et al. (2024) reviewed 55 studies on industrial peak shaving and tested a threshold-based battery strategy in a Malaysian food factory, where one month of measurements showed 6.9% lower energy cost and 8.6% lower CO2 emissions.

Rule-based control is transparent and easy to deploy, which is why it also serves as the benchmark in several other studies (Amini et al., 2023; Gao et al., 2021; Kanaan et al., 2023; Upadhyay et al., 2024). Its weakness is that it reacts to the current interval only and cannot prepare for a cloudy afternoon or an evening demand peak. The reported savings are, moreover, difficult to compare: the reference cases differ, the systems are small, and the evidence is either short or laboratory-based.

### 3.3.3 Optimization-based scheduling

Miah et al. (2022) analyzed 110 highly cited microgrid papers published between 2010 and 2021, compared 24 storage controllers and 21 optimization schemes, and identified limitations and research gaps in the selected papers. Among the primary studies, Kanaan et al. (2023) feed LSTM forecasts of load and PV into a mixed-integer linear programming (MILP) schedule that is re-solved every 15 minutes from live measurements under state-of-charge and state-of-health limits; the daily cost was 9.2% lower than with a heuristic controller and 3.5% lower than with a stochastic method. Amini et al. (2023) add a linearized aging cost to an MPC-style MILP and, compared with a simple controller, reduced battery capacity fade by 5.06% and degradation cost by 4.67% while raising profit by 1.10%. Georgiadis et al. (2025) combine Transformer and MLP forecasts with a 24-hour MILP for a Greek manufacturing plant with 2 MW of PV; a 1 MW / 2 MWh battery reduced the daily cost by up to 352 relative monetary units, with a payback of about seven years that shortens with a subsidy.

These studies indicate that explicit constraints combined with forecasts yield gains over simple controllers. The evidence base is nevertheless narrow: Kanaan et al. use residential data and a plant with a diesel generator, Amini et al. study a PV farm selling in a market, and Georgiadis et al. evaluate four representative days at hourly resolution. In all three, the objective is expressed mainly in monetary terms (with emissions priced in two of them) rather than as the share of solar energy used on site.

### 3.3.4 Forecasting with machine learning

Almost every optimization study depends on forecasts. Gao et al. (2021) combine a GAN-LSTM PV forecast with a simple-average load forecast, Kanaan et al. (2023) use stacked LSTM networks, Georgiadis et al. (2025) use Transformer-based and MLP models, and Upadhyay et al. (2024) use a random forest for load. A common finding is that schedule quality is limited by forecast quality: Gao et al. report a large PV forecast error, and Georgiadis et al. note that the PV forecast deteriorates when the weather changes suddenly. The contribution of a sophisticated forecast relative to a trivial one, such as repeating the previous day, is generally not reported separately, so it remains unclear how much of the final result the forecasting model explains.

### 3.3.5 Reinforcement learning

Reinforcement learning (RL) learns a dispatch policy from interaction with a simulated system. In the industrial park studied by Gao et al. (2021), greedy rules, a genetic algorithm, and DDPG reduced cost by 18.9%, 36.1%, and 35.9%, respectively; deep RL therefore matched but did not outperform the evolutionary method. Upadhyay et al. (2024) tested PPO with a random-forest load forecast on an industrial microgrid in Norway (200 kWp PV, 1.1 MWh battery) and obtained about 20% more monthly saving than a logic-based benchmark over six months. Jung et al. (2025) used two cooperating PPO agents, one for cost and one for charge and discharge switching, on an industrial building with 250 kW of PV and 1000 kWh of storage at 15-minute steps; cost fell by 14.68% against a case without storage, and switching events were 35.2% fewer than with single-agent PPO over a five-day test period.

RL adapts without an explicit system model and acts quickly once trained. Its drawbacks for the present project are long training (50 million steps in Upadhyay et al., 2024), reliance on simulation, untested scalability, and decisions that are typically difficult to explain to an operator who must approve each recommendation.

### 3.3.6 Battery wear and hybrid storage

Cycling shortens battery life, and several studies therefore treat wear explicitly. Amini et al. (2023) price calendar and cycle aging, Jung et al. (2025) use the number of switching events as a proxy, and Georgiadis et al. (2025) include aging and replacement in a simplified form in the investment analysis. Benavides et al. (2022) tested ramp-rate and moving-average power smoothing on laboratory hardware with supercapacitor and lithium-ion storage and showed that the control strategy changes the number of supercapacitor cycles. Their work concerns power quality with PV, wind, and hydrokinetic sources rather than energy cost, so it supports only the general point that the control logic determines battery cycling.

## 3.4 What is already known

First, coordinating PV generation, load, and battery storage reduces grid purchases and cost. Reported reductions range from 6.9% (Zahari et al., 2024) to about 88% (Kermani et al., 2021), but they depend on system size, tariff, and reference case and cannot be pooled.

Second, forecast-based optimization and learning methods outperform simple rules where the two are compared directly. Examples are a 9.2% lower daily cost than a heuristic (Kanaan et al., 2023) and about 20% more monthly saving than a logic benchmark (Upadhyay et al., 2024); in an industrial park, optimized dispatch nearly doubled the cost reduction of greedy rules (Gao et al., 2021).

Third, battery wear should be treated as an explicit constraint or cost, because aging models change when and how deeply the battery is cycled (Amini et al., 2023; Kanaan et al., 2023).

Fourth, economic viability depends on battery price and tariffs. A payback of about seven years is reported in two studies (Georgiadis et al., 2025; Kermani et al., 2021), Gao et al. (2021) find that storage pays off only below a battery price threshold, and IRENA (2025) documents a steep decline in storage costs.

## 3.5 Limitations of existing work and their treatment in the project

Table 3.2 lists the main limitations found in the reviewed studies and shows how the project responds to each. The responses follow the scope and assumptions of the project proposal: a software-only prototype that gives recommendations and does not control equipment.

**Table 3.2.** Limitations in the literature and their treatment in the project

| Limitation in the literature | Evidence in the reviewed sources | How the project takes it into account |
| --- | --- | --- |
| **Little and short evidence from real industrial sites** | One month of data (Zahari et al., 2024); six months (Upadhyay et al., 2024); four representative days (Georgiadis et al., 2025); a five-day test (Jung et al., 2025); laboratory scale (Kermani et al., 2021). | The prototype uses simulated or open data and makes no claim of real-world improvement. It is evaluated in four defined scenarios: high solar generation, low solar generation, high facility demand, and limited battery capacity. |
| **Proxy data from other settings** | Residential homes (Kanaan et al., 2023); a PV farm in a market (Amini et al., 2023); a laboratory with wind and hydrokinetic sources (Benavides et al., 2022). | The input is a facility file of solar power and facility load at hourly resolution; the file is checked, and forecast accuracy is shown against meter readings. |
| **Forecast value not isolated from simple benchmarks** | Forecasts feed the optimization, but their gain over a trivial forecast is generally not reported separately in the reviewed studies. | A "same as yesterday" forecast is calculated next to the main forecast, and the forecast error of both is reported. |
| **Simplified battery wear** | Linearized aging (Amini et al., 2023); switching count as a proxy (Jung et al., 2025); simplified degradation (Georgiadis et al., 2025). | Battery power limit, allowed charge range and a daily cycle limit are hard constraints. No electrochemical aging model is built; this is stated as a simplification. |
| **Objectives tied to markets and tariffs** | Spot market (Gao et al., 2021); price arbitrage and market profit (Amini et al., 2023; Georgiadis et al., 2025); national tariff (Jung et al., 2025). | The objective is the share of solar energy used or stored on site and lower grid import. Tariffs and market trading are outside the project. |
| **Opaque methods and heavy training** | Training of 50 million steps and untested scalability (Upadhyay et al., 2024); no cost advantage of deep reinforcement learning over a genetic algorithm (Gao et al., 2021). | A transparent optimization gives a reason for every interval, and the energy specialist accepts or rejects each recommendation. The prototype advises only and does not control equipment. |
| **Coarse time resolution** | Hourly steps (Gao et al., 2021; Georgiadis et al., 2025). | The plan uses hourly intervals, because the specialist did not specify the data interval. The step is stated in every run, and a finer step can be used if the file provides it. |
| **Forecasts degrade in sudden weather change** | Weaker PV forecasts when the weather changes (Georgiadis et al., 2025); a large PV forecast error (Gao et al., 2021). | A solar irradiance forecast is used as an input when available, and the displayed forecast error warns the user when the day was hard to predict. |

*Source: compiled by the authors from the reviewed publications and the project proposal.*

Within the reviewed sources, no study was found that combines a transparent optimization, day-ahead forecasts at hourly resolution, an explicit comparison with both a rule-based baseline and a naive forecast, and a recommendation that an energy specialist can accept or reject. The project addresses this combination while limiting its claims to simulation and open data, in line with the available evidence. Its effectiveness is measured by six indicators: solar energy utilization rate, grid electricity consumption, surplus solar energy, algorithm correctness, system usability, and forecast error.

## References

Amini, M., Nazari, M. H., & Hosseinian, S. H. (2023). Predictive energy management strategy for battery energy storage considering battery degradation cost. *IET Renewable Power Generation, 17*(5), 1119–1138. [https://doi.org/10.1049/rpg2.12669](https://doi.org/10.1049/rpg2.12669)

Benavides, D., Arévalo, P., Tostado-Véliz, M., Vera, D., Escamez, A., Aguado, J. A., & Jurado, F. (2022). An experimental study of power smoothing methods to reduce renewable sources fluctuations using supercapacitors and lithium-ion batteries. *Batteries, 8*(11), 228. [https://doi.org/10.3390/batteries8110228](https://doi.org/10.3390/batteries8110228)

Gao, Y., Li, J., & Hong, M. (2021). Machine learning based optimization model for energy management of energy storage system for large industrial park. *Processes, 9*(5), 825. [https://doi.org/10.3390/pr9050825](https://doi.org/10.3390/pr9050825)

Georgiadis, G. P., Dimitriadis, C. N., Passalis, N., & Georgiadis, M. C. (2025). A hybrid ML-MILP framework for the optimal integration of photovoltaic and battery systems in manufacturing industries. *Computers & Chemical Engineering, 203*, 109356. [https://doi.org/10.1016/j.compchemeng.2025.109356](https://doi.org/10.1016/j.compchemeng.2025.109356)

International Energy Agency. (2024). *Batteries and secure energy transitions* (World Energy Outlook Special Report). IEA. [https://www.iea.org/reports/batteries-and-secure-energy-transitions](https://www.iea.org/reports/batteries-and-secure-energy-transitions)

International Renewable Energy Agency. (2025). *Renewable power generation costs in 2024*. IRENA. [https://www.irena.org/Publications/2025/Jul/Renewable-Power-Generation-Costs-in-2024](https://www.irena.org/Publications/2025/Jul/Renewable-Power-Generation-Costs-in-2024)

Jung, S.-W., An, Y.-Y., Suh, B., Park, Y., Kim, J., & Kim, K.-I. (2025). Multi-agent deep reinforcement learning for scheduling of energy storage system in microgrids. *Mathematics, 13*(12), 1999. [https://doi.org/10.3390/math13121999](https://doi.org/10.3390/math13121999)

Kanaan, L., Ismail, L. S., Gowid, S., Meskin, N., & Massoud, A. M. (2023). Optimal energy dispatch engine for PV-DG-ESS hybrid power plants considering battery degradation and carbon emissions. *IEEE Access, 11*, 58506–58515. [https://doi.org/10.1109/ACCESS.2023.3281562](https://doi.org/10.1109/ACCESS.2023.3281562)

Kermani, M., Adelmanesh, B., Shirdare, E., Sima, C. A., Carnì, D. L., & Martirano, L. (2021). Intelligent energy management based on SCADA system in a real microgrid for smart building applications. *Renewable Energy, 171*, 1115–1127. [https://doi.org/10.1016/j.renene.2021.03.008](https://doi.org/10.1016/j.renene.2021.03.008)

Miah, M. S., Lipu, M. S. H., Ansari, S., Meraj, S. T., Hasan, K., Masaoud, A., Hussain, A., Mahmud, M. S., & Bashar, S. S. (2022). Energy storage controllers and optimization schemes integration to microgrid: An analytical assessment towards future perspectives. *IEEE Access, 10*, 52982–53014. [https://doi.org/10.1109/ACCESS.2022.3174123](https://doi.org/10.1109/ACCESS.2022.3174123)

Upadhyay, S., Ahmed, I., & Mihet-Popa, L. (2024). Energy management system for an industrial microgrid using optimization algorithms-based reinforcement learning technique. *Energies, 17*(16), 3898. [https://doi.org/10.3390/en17163898](https://doi.org/10.3390/en17163898)

Zahari, N. E. M., Mokhlis, H., Mubarak, H., Mansor, N. N., Sulaima, M. F., Ramasamy, A. K., Zulkapli, M. F., Ja'apar, M. A. B., Jaafar, M., & Marsadek, M. B. (2024). Integrating solar PV, battery storage, and demand response for industrial peak shaving: A systematic review on strategy, challenges and case study in Malaysian food manufacturing. *IEEE Access, 12*, 106832–106856. [https://doi.org/10.1109/ACCESS.2024.3420941](https://doi.org/10.1109/ACCESS.2024.3420941)
