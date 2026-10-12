# Interview guide

Use this in a 20–30 minute call. Ask the questions in order, then follow one or two answers that contradict the proposal. Write the notes the same day in [interview-log.md](interview-log.md).

Do not ask for passwords, single-line diagrams of a live plant, or identifiable load traces in the first meeting. If the person offers anonymous or aggregated data later, record the offer and the conditions. Do not commit the data file until the team and the supervisor agree it contains no personal or commercial secrets.

## Opening (2 minutes)

State the project in one sentence: a day-ahead battery schedule for one factory with solar, aimed at using more of that solar on site, reviewed by an energy manager before any equipment is commanded.

Say that notes will be stored in the project repository under their role and organisation, not under a private story, and that they can skip any question. Point them at [consent-note.md](consent-note.md) if they want the written version.

## Questions

1. What is your role, and what kinds of sites do you work with (factory, warehouse, solar plant, battery supplier, developer)?
2. On sites you know that have solar, what happens to generation the site cannot use at that moment? Export, curtailment, or something else?
3. Do those sites have a battery? If yes, what is it for: backup, shifting solar, cutting a demand peak, or a mix?
4. Who decides when the battery charges and discharges? A person, a clock schedule, or software from the inverter or battery vendor?
5. What goes wrong with that arrangement? Ask for a concrete shift, season, or bill item, not a general complaint.
6. Which limits are non-negotiable: power, state of charge, temperature, number of cycles, warranty terms, export limit?
7. What data exists in practice at 15-minute or hourly resolution: PV power, site load, battery state, tariff, weather? What is missing?
8. If a tool proposed tomorrow’s battery schedule, what would make you trust it, and what would make you ignore it?
9. Which result matters more on the sites you know: solar used on site, the energy bill, the demand peak, or backup during an outage?
10. Who else should we talk to, especially a facility energy manager?

## What to listen for

| If they say | Effect on the project |
| --- | --- |
| Surplus solar is routinely exported or curtailed | Supports the problem statement. Mark it verified for that class of site only |
| Batteries are mainly for outages, not for shifting solar | The self-consumption aim may be secondary. Record this before changing requirements |
| Scheduling is a vendor black box | Supports the need for an explainable recommendation. Does not prove the vendor product is incapable |
| Nobody will share 15-minute data | The evaluation plan must use a documented public or synthetic series |
| Demand charges dominate the bill | Peak demand may need a higher priority than the proposal currently gives it. Change the objective only after two independent conversations agree |
| The user is an installer, not an energy manager | Revisit the primary actor in the use-case diagram |

## Closing

Ask whether they are willing to be named as “engineer at [organisation]” in the diploma text. If not, cite the organisation only, or “a battery supplier in Kazakhstan” if even that is too specific. Thank them. Offer to send the one-page problem statement after the pre-defense if they want it.
