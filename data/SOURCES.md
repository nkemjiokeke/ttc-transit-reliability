# Sources - Project 05: TTC Transit Reliability (real Toronto Open Data)

All data is real, from the City of Toronto Open Data Portal, under the Open Government Licence - Toronto. No simulation.

## The dataset
- **TTC Subway Delay Data** - one row per delay incident: Date, Time, Day, Station, Code (delay reason), Min Delay, Min Gap, Bound, Line, Vehicle.
  https://open.toronto.ca/dataset/ttc-subway-delay-data/
- **Delay code lookup** - the "readme" / "codes" file on the same dataset page translates each Code into a plain description (e.g., a mechanical fault, a passenger-related delay, a signal problem). You need this to group causes.

## What to download
1. Go to the dataset page above.
2. Download the yearly Excel files for the most recent complete years - start with **2023 and 2024** (add 2025 if you want the latest partial year). Each year is one .xlsx.
3. Download the **delay codes / readme** file (the code-to-description lookup).
4. Save all of them into this `data/` folder.

## Notes
- `Min Delay` is the minutes of delay to the schedule for that incident; `Min Gap` is the minutes between trains. `Min Delay` is the one to sum for "lost minutes".
- A blank or zero `Min Delay` row is a logged event that did not actually delay service - keep it out of the delay totals.
- Codes are grouped into families in the lookup (mechanical, passenger, signals/track, security, staffing, weather). We will roll individual codes up into these families for the "why" analysis.
- The two subway lines that carry almost all the volume are Line 1 (Yonge-University) and Line 2 (Bloor-Danforth); Lines 3 and 4 are small.
