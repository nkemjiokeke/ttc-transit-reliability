# Project 05 - TTC Transit Reliability: where Toronto's subway loses its minutes

### Build guide (real Toronto Open Data; you build it, this is the map)

Goal: take every subway delay in Toronto and find where the lost minutes actually concentrate - which line, which stations, which causes, and which times - so the TTC can spend a limited maintenance and operations budget on the small number of things that cause most of the delay. Built entirely on real open data.

## 1. The situation
The TTC subway is the spine of Toronto's transit, and its reliability has been a running public issue: riders report frequent delays, and the agency is under pressure to hit service targets on a tight budget. Every delay is logged with a cause code, a location, and the minutes of delay. That log is enough to move the conversation from "the subway is unreliable" to "here are the specific stations, causes, and hours that produce most of the lost time, and here is where to act first."

**The one-sentence problem:** the TTC knows service is delayed but does not have a clear, ranked picture of where the delay minutes come from, so it cannot target the fixes that would recover the most time.

## 2. Decision-maker
- **Primary:** the **TTC's service planning and maintenance leadership**, who decide where to put maintenance crews, signal upgrades, and staffing.
- **Secondary:** the **city and the TTC board** (accountability and budget), and riders (who feel the reliability).

They want a ranked answer: if we can only fix a few things this year, which stations, causes, and times give back the most minutes.

## 3. Problem statement
Delay is treated as one big number. This project breaks the total delay down by line, station, cause, and time of day, finds where it concentrates, and turns that into a short list of targets that would recover the most delay minutes.

## 4. Key questions
1. How big is the problem? Total delay minutes per year, the trend, and the average delay per incident.
2. Where does it concentrate by location? Delay minutes by line and by station - is it a few stations or spread evenly?
3. Why does it happen? Delay minutes by cause family (mechanical, passenger, signals/track, security, staffing, weather). Which causes cost the most time, not just the most incidents.
4. When does it happen? Delay by hour of day and day of week - how much lands in the rush hours when it hurts the most riders.
5. The 80/20: do a small number of stations and causes drive most of the lost minutes?
6. So what? The ranked list of station-and-cause targets that would recover the most delay, and where the TTC should act first.

## 5. Data model
One fact table at delay-incident grain: the subway delay rows (see `data/SOURCES.md`). Join to the delay-code lookup to get a plain description and a cause family.

Derived fields to build early:
| Field | Definition |
|---|---|
| `hour` | hour of day from the Time field |
| `peak` | 1 if hour in the AM (7-9) or PM (16-19) rush, else 0 |
| `cause_family` | code rolled up into mechanical / passenger / signals-track / security / staffing / weather |
| `is_delay` | 1 if Min Delay > 0 (drop logged events with no actual delay) |

## 6. KPIs
| KPI | Definition | Why it matters |
|---|---|---|
| Total delay minutes | sum of Min Delay | The headline lost time. |
| Delay per station | delay minutes by station | Where to send crews. |
| Delay by cause family | delay minutes by cause | What to fix. |
| Peak-hour share | delay minutes in rush / total | Delay that hits the most riders. |
| Concentration | share of minutes from the top 10 stations / top 5 causes | Is it a few problems or many. |
| Incidents vs minutes | count vs summed minutes | Separates frequent-but-short from rare-but-long. |

The distinction that matters: a cause can be common but short, or rare but long. Rank by **minutes**, not incident count, because minutes are what riders lose.

## 7. Build it - step by step
- **Excel / Power Query:** stack the yearly files, clean the Time field into an hour, join the code lookup, add the cause family and peak flag. Drop the zero-delay rows from the delay totals.
- **SQL (SQLite):** the engine. One query per key question - totals and trend, by line, by station, by cause family, by hour, and the 80/20 concentration.
- **Python (optional):** a heat map of delay by hour and day, and the Pareto curve.
- **Datawrapper / Power BI:** the reliability dashboard and the publication charts.

## 8. Charts
| Question | Chart |
|---|---|
| How big and trend | delay minutes by year (line/bar) |
| Where - stations | top stations by delay minutes (bar / Pareto) |
| Why - causes | delay minutes by cause family (bar) |
| When | delay by hour x day (heat map) |
| Concentration | cumulative share by station (Pareto curve) |
| The targets | ranked station-and-cause table |

## 9. Recommendation and impact
A short list of targets - the stations, causes, and times that hold most of the delay - with the delay minutes each would recover if addressed, so the TTC can act where the time is, not where the noise is.

## 10. Limitations
The log records the cause the TTC assigned, which can be coarse or inconsistent. Delay minutes are schedule delay, not total rider-minutes lost (a delay in rush hour affects far more people than the same delay at midnight - the peak-hour cut is a partial answer to that). The data is subway only here; bus and streetcar are separate files that could extend the study. It shows where delay concentrates, not the engineering cost of fixing each cause.
