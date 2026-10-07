# Project 05 - LinkedIn write-up (TTC transit reliability)

## LinkedIn post (connected story, first person)

I pulled every delay the Toronto subway logged over the last two and a half years, about 24,500 of them, and worked out where the lost time actually comes from. It added up to 192,000 minutes, roughly 3,200 hours of delay.

The first finding went against what I assumed. The subway is not mostly delayed by breaking down. Equipment faults are 8% of the lost minutes. Almost two-thirds are people-related: medical events, disorder, assaults, and passenger alarms. Track, signals and power make up another fifth, and those are the longest delays, over nine minutes each on average.

The delay concentrates on the busiest line. Line 1 holds 55% of the lost minutes, so a minute saved there reaches the most riders.

Then I went looking for the usual suspects and did not find them. I expected a few bad stations, but the worst is only 3% of the total and it takes about twenty stations to reach 40%, so the delay is spread across the whole network. I expected a rush-hour pattern, but the lost minutes are close to flat all day, with bumps in the afternoon and at start-of-service around 5am.

That changes the recommendation. You cannot fix a station or a time window, because the delay is not in any of them. It is in the cause. Most of it is what happens with people on the system, spread evenly and concentrated only on Line 1. So the lever is response capacity, not more maintenance: staff, safety, and medical response where the minutes are, plus separate attention to the rare but long track and signal failures.

I cleaned the data in Power Query, built the analysis in SQL, and built the dashboard in Power BI so a planner can filter by line, cause, and time.

The data is real, from the City of Toronto's open data. Subway only, and the cause is whatever the TTC logged, so I read it as where the time goes, not a verdict on blame.

## Carousel slides

1. Where does the Toronto subway lose its time? Every logged delay, 2024 to 2026. Real City of Toronto open data, SQL and Power BI.
2. The scale. About 24,500 delays, 192,000 minutes, roughly 3,200 hours of lost service.
3. It is people, not breakdowns (Chart 1). Medical, security and disorder are 63% of lost minutes. Equipment is 8%.
4. It sits on Line 1 (Chart 2). Line 1 carries 55% of the delay, Line 2 another 41%.
5. There is no hotspot (Chart 3). The worst station is 3% of the total; it takes about 20 stations to reach 40%. The delay is network-wide.
6. It runs all day (Chart 4 / heat map). Lost minutes are flat from morning to midnight, with bumps at the afternoon and at start-of-service around 5am.
7. Rare but long (Chart 5). Track and signal failures average over nine minutes each, the longest of any cause.
8. The dashboard. Built in Power BI so a planner can filter delay by line, cause, and time, and read it by hour and day. [insert Power BI screenshot]
9. The call. Response capacity, not more maintenance: staff and safety where the minutes are, on Line 1 and across the network, plus separate work on the long track and signal failures.
