# 10. Project Management and Risks

## 10.1 Git repository

The project uses a GitHub repository located at [SolarEnergyDiplomaAITU2027](https://github.com/MegaSlime-2407/SolarEnergyDiplomaAITU2027). The repository is private; all team members, the supervisor, and the committee have access. Each student commits under his or her own account. The README.md file contains the project title, problem statement, team and responsibilities, scope and status, technologies, and links to YouTrack and the documents. The folders are docs (proposal, literature review, comparisons, requirements, architecture, verification plan, project management, supervisor feedback), diagrams (editable sources and exports), prototype, src, tests, and config. Passwords, keys, and personal data are not committed.

Work is committed progressively. The name of every branch and the first words of every commit message are the YouTrack task key (for example, `SSS-13-battery-constraints` and "SSS-13: Add battery limits to the requirements"). Changes enter the main branch only through a pull request that explains the change and how it was checked and that another team member reviews. Each submission is marked with a tag (`pre-defense-1`, `pre-defense-2`, and `final-pre-defense`) that is not moved afterwards.

## 10.2 YouTrack project

The tasks are managed in the YouTrack project smart-solar-storage (key SSS) on the agile board "smart-solar-storage 001", sprint 001. Each task has the type Task, one assignee, a due date, a priority (Must, Should, or Could), a state (To Do, In Progress, On Hold, In Review, or Done), the expected outcome, and acceptance criteria. A task is marked Done only when its acceptance criteria are met, and its description links to the pull request or the deliverable. Table 10.1 lists the deliverables of the first pre-defense.

**Table 10.1.** YouTrack tasks for the first pre-defense

| Task | Deliverable | Responsible |
| --- | --- | --- |
| **SSS-1** | Project proposal | Yun V. |
| **SSS-2** | Evidence of the relevance | Yun V. |
| **SSS-3** | Literature review | Mussagali K. |
| **SSS-4** | Existing system comparison | Mussagali K. |
| **SSS-5** | Technology comparison | Oralov A. |
| **SSS-6** | Architecture and diagrams | Oralov A. |
| **SSS-7** | UX / prototype | Yun V. |
| **SSS-8** | Verification and evaluation plan | Oralov A. |
| **SSS-12** | Project management and risks | Mussagali K. |

*Note. Source: compiled by the authors from the YouTrack project.*

## 10.3 Allocation of responsibilities

Table 10.2 shows the role of each team member and who reviews the work. The supervisor is Nursultan Khaimuldin.

**Table 10.2.** Roles and responsibilities

| Team member | Role and responsibilities |
| --- | --- |
| **Oralov Alinur Kairgazyuly (SE-2407)** | Backend; DevOps (deployment of the project on a server); work with the data and the effectiveness algorithm |
| **Yun Violetta Dmitrievna (SE-2408)** | Frontend: mobile application (Flutter and Dart) |
| **Mussagali Kundyz Ardakkyzy (SE-2408)** | Web interface (HTML, CSS, JavaScript); coordination of project management |

*Note. Source: compiled by the authors.*

## 10.4 Milestones

The project has three submission milestones. Each is identified by a Git tag, and its completion is checked against the YouTrack tasks assigned to it. Unfinished tasks are listed as outstanding in the submission and moved to the next milestone with a new deadline.

**Table 10.3.** Project milestones

| Milestone | Planned deliverables | Evidence |
| --- | --- | --- |
| **M1 Pre-defense 1** | README; proposal and scope; evidence of relevance; literature review; existing system comparison; technology comparison; requirements; architecture diagrams with editable sources; prototype materials; verification and evaluation plan; YouTrack link | Tag `pre-defense-1` |
| **M2 Pre-defense 2** | Algorithm and baseline on test data; backend and database; web prototype connected to the backend; first results of the test scenarios | Tag `pre-defense-2` |
| **M3 Final pre-defense** | Mobile application; deployed system; all test scenarios and indicators evaluated against the baseline; final documentation with known limitations | Tag `final-pre-defense` |

## 10.5 Dependencies

**Table 10.4.** Dependencies of the project

| Dependency | Type | Handling |
| --- | --- | --- |
| **D1** Requirements, architecture, implementation, testing, and evaluation follow one another | Internal | Fix mandatory requirements at the second pre-defense; later changes go through a YouTrack task |
| **D2** Test data (solar power and facility load) from simulated or open datasets | External | Choose and describe the datasets early; keep one agreed file format |
| **D3** Results of the backend are used by the web platform and the mobile application | Internal | Fix the interface format before client work starts |
| **D4** Availability of the supervisor and of user representatives | External | Book dates in advance and record them in YouTrack |
| **D5** Access of the supervisor and the committee to the repository and YouTrack | External | Check access before every pre-defense |
| **D6** A server for deployment | External | Prepare instructions for a local run as an alternative for demonstrations |

## 10.6 Risks

The team rated the likelihood and impact of each risk as Low, Medium, or High. The register is reviewed at every milestone, and a risk that materializes is recorded as a YouTrack task.

**Table 10.5.** Risk register

| ID | Risk | Likelihood | Impact | Mitigation |
| --- | --- | --- | --- | --- |
| **R1** | Only simulated or open data are available, so results may not reflect a real facility | High | Medium | State this limit in all documents; make no claim of real-world improvement; test contrasting scenarios |
| **R2** | Weak input data or forecast error on days with sudden weather change lowers the quality of recommendations | Medium | Medium | Show the forecast error next to the results; keep battery limits valid whatever the forecast |
| **R3** | The scope is too large for three students (algorithm, backend, web, mobile) | Medium | High | Fix the order of priority (algorithm and data, then web, then mobile); keep the system advisory only; re-plan at the second pre-defense |
| **R4** | Backend, deployment, data, and the algorithm are the work of one team member | High | High | A second member reviews every pull request of these tasks; keep run and setup instructions in the README; rebalance work at the second pre-defense |
| **R5** | Evidence of relevance is insufficient because the planned user discussions are not completed | Medium | High | Schedule 3–5 discussions as YouTrack tasks with dates; record findings separately from assumptions |
| **R6** | YouTrack tasks lack an assignee, deadline, or acceptance criteria, so work cannot be traced | Medium | Medium | Check all tasks at the end of each sprint; do not mark a task Done without a link to its pull request or deliverable |
| **R7** | Feedback from the supervisor or from users arrives late | Medium | Medium | Agree checkpoint dates in advance; send materials before each checkpoint; record decisions as tasks |
| **R8** | The server for deployment is unavailable or deployment is delayed | Medium | Medium | Demonstrate the system locally; keep deployment as a separate task with its own acceptance criterion |

## 10.7 Next steps

**Table 10.6.** Next steps

| No. | Step | Responsible |
| --- | --- | --- |
| **1** | Complete the YouTrack tasks (assignee, due date, priority, type, acceptance criteria) and create the tasks for the requirements specification and the supervisor feedback | Mussagali K. |
| **2** | Prepare the submission for pre-defense 1: tag `pre-defense-1`, summary, known limitations, outstanding tasks | Yun V. |
| **3** | Record the supervisor's feedback on pre-defense 1 and turn each decision into a YouTrack task | All members |
| **4** | Complete 3–5 discussions with user representatives; update requirements and acceptance criteria | Yun V. |
| **5** | Select and describe the test datasets (solar power and load); fix the input file format | Oralov A. |
| **6** | Implement the "same as yesterday" forecast, the rule-based baseline, and the checks of energy balance and battery limits | Oralov A. |
| **7** | Implement the gradient-boosted forecast and the linear optimization of battery charge and discharge | Oralov A. |
| **8** | Design the database schema and the interface for forecasts and plans; prepare the Docker configuration | Oralov A. |
| **9** | Turn the prototype into web pages connected to the backend | Mussagali K. |
| **10** | Prepare the submission for pre-defense 2: tag, summary, known limitations, outstanding tasks | All members |
| **11** | Run the four test scenarios and collect the six indicators for the main method and the baseline | All members |
| **12** | Build the mobile application on the same interface | Yun V. |
| **13** | Deploy the system on a server with Docker and nginx | Oralov A. |
