# 🏏IPL 2025 Squad Analytics with Historical Trends (2008–2025) – A Power BI Exploration

[![View Dashboard](https://img.shields.io/badge/View%20Dashboard-%23000000.svg?style=for-the-badge&logo=Codeforces&logoColor=gold)](https://app.powerbi.com/view?r=eyJrIjoiMDYyZGU5OWItZjliMC00NjE5LWFhMmEtMGI1OGZkMDE4NTJhIiwidCI6IjQ2NTRiNmYxLTBlNDctNDU3OS1hOGExLTAyZmU5ZDk0M2M3YiIsImMiOjl9)

<a href="https://datascienceportfol.io/deerajS" target="_blank"><img width="167" height="200" alt="Image" src="https://github.com/user-attachments/assets/3badf33e-c36c-4088-bb3f-b0ed49e15fac" />
</a>

## Table of Contents
  - [Problem Statement](#problem-statement)
  - [Project Planning using Star Method](#project-planning-using-star-method)
  - [Data Source](#data-source)
  - [Data Preprocessing \& ETL](#data-preprocessing--etl)
  - [Data Modelling](#data-modelling)
  - [Data Analysis](#data-analysis)
  - [Dashboard](#dashboard)
  - [Findings](#findings)
  - [Tools And Softwares](#tools-and-softwares)


## Problem Statement
<details>
<summary>
$\textsf{\color{blue}{View Problem Statement ➡️}}$
</summary><br>

**Problem**

Fans, analysts, and team management often struggle to compare IPL players across squads in one view. Key challenges include:

- Tracking batting & bowling stats across different players.

- Identifying top performers (Runs, Wickets, Strike Rate, Economy).

- Filtering by teams and comparing players side by side.

- Limited visibility into season-level contributions of each squad.

**Challenges:**

Build a Squads Analytics Page in Power BI that:

1. Data Integration from Multiple Sources

- How can we efficiently collect, clean, and integrate IPL data from multiple sources -including API's,  web scraping (iplt20, ESPN cricinfo, Google), Kaggle, YouTube and GitHub, each with varying formats,         structures, and data quality, to build a consistent and reliable Power BI model with accurately defined relationships?
- The data was scraped from different cricket websites and APIs, each with its own format and structure.
- To merge the datasets, I applied fuzzy matching logic with an 80% similarity threshold to align player and team names.
- Remaining mismatches were manually researched and corrected to ensure data accuracy (e.g., resolving player name variations and missing records).

2. Data Cleaning & Standardization

- Player and team names appeared in different formats across sources.

- Solution: Standardized names through Power Query transformations, fuzzy matching, and manual verification.

3. Complex Data Modelling

- Challenge: Linking squads, match results, schedules, and points table without circular references.

- Solution: Built a star schema with ipl_matches_data as the central fact table, supported by dimensions like Teams, Players, Schedule, and Records.

4. Dynamic Filtering Across Pages

- Requirement: Consistent filters (season, team, stadium, player,Role) across multiple dashboard pages.

- Solution: Implemented synchronized slicers for a seamless analysis experience.

- Displays full team squads with logos & player profiles.

- Provides individual player cards (Batting + Bowling stats).

- Highlights captains, key performers, and role distribution.

</details>


## Project Planning using Star Method
<details>
<summary>
$\textsf{\color{blue}{View Stratergy ➡️}}$
</summary><br>

### 📝 S - Situation

The IPL has 10 teams, each with a large squad of players. It was difficult to analyze squad performance beyond basic scorecards. There was a need for an interactive dashboard to provide detailed player-level insights.

Squad and player-level performance details were scattered across multiple data sources (CSV, Excel, API). Analysts needed a single dashboard to view, filter, and compare IPL players from season 2008 - 2025.

### 🎯 T - Task

Develop a Power BI dashboard page (Squads) that:

- Highlights star performers.
- Displays team squads with roles (Batter, Bowler, All-Rounder, WK).

- Provides player cards with batting & bowling stats.

- Identifies captain and key performers with analytics charts.

### ⚡ A - Action

- Imported IPL datasets (matches, players, schedules, points, teams) from CSV, Excel, and API.

- Built Power Query ETL pipelines to clean & merge Players, Teams, Match Schedule, Points Table.

- Designed Fact + Dimension data model for squads and stats.

- Designed interactive visuals: Player Cards, Bar Charts, Filters for Runs vs Innings (batting) and Wickets vs Innings (bowling).

- Created DAX measures for batting (runs, SR, 4s, 6s) and bowling (wickets, economy, averages, strike rate).

Designed Power BI visuals:

- Player Profile Cards (Batting + Bowling).

- Captain  and Players Highlight Cards.

- Team Filters with Logos.

- Comparison Charts (Runs vs Innings, Wickets vs Matches).

### 🏆 R - Result

- Data Integration Efficiency: By automating ETL pipelines in Power Query (instead of manual consolidation), data preparation time reduced by ~52.7%.

- Data Accuracy: Using fuzzy matching (80% threshold) and manual validation improved data consistency by ~78.3%, reducing mismatched player/team records.

- Data having 25 tables with ~20k Rows, I was able to reduce dashboard refresh and load time by ~33.2% using  Performance Optimization techniques. 

- Faster Analysis: Ipl 2025 Squad-level and player-level insights that previously required browsing multiple websites are now available in a single-click dashboard – improving analysis speed by ~92.6%.

- Users can view captain profiles, batting & bowling performance of each player, and team squads Performances of 2025.

- Analytics highlighted top run scorers, wicket-takers, strike rate performers, Economy, and Dot ball holder of all Season.
- Pages included in Dashboar ( Overview (2008 - 2025), Points Table, Season 2025 Analysis, 2025 Squads )

</details>

## Data Source
<details>
<summary>
$\textsf{\color{blue}{View Data Source ➡️}}$
</summary><br>

- IPL Matches Data (CSV) → Match-level details (id, season, teams, winner, venue).

- Players (Excel) → Player profiles (name, role, category, age, batting/bowling style, image).

- Teams (CSV) → Team IDs, names, short codes, logos.

- Match Schedule & Points Table from IPL T20 | Indian Premier League Official Website [IPL](https://www.iplt20.com/)

- Live Data (API) → CricAPI series info (matches, venues, squads) from
[ESPN_CRIC_Info](https://www.espncricinfo.com/)

- Other Data sets from Kaggle.

</details>


## Data Preprocessing & ETL

<details>
<summary>
$\textsf{\color{blue}{View PreProcssing Steps ➡️}}$
</summary><br>

The raw datasets were cleaned and transformed in Power Query (M).

**Steps Performed**

**1.IPL Matches Data (CSV)**

- Promoted headers, fixed data types.

- Removed unused columns (stage).

- Merged with teams_data to fetch team short names & logos.

**2. Match Schedule (Excel)**

- Cleaned nulls & placeholders (NO_Result).

- Standardized stadium names.

- Created Stadium LOC by merging stadium + city.

**3. Points Table (Excel)**

- Converted season column into SEASON & SEASON_ID.

- Standardized column types.

- Added team logos & codes.

**4. Players Data (Excel)**

- Cleaned duplicates and fixed name inconsistencies.

- Merged with Teams table to fetch team logos.

- Merged with Captains Table to flag captains.

**5. Teams Data (CSV)**

- Standardized team IDs, names, abbreviations, and image URLs.

**6. CricAPI (JSON API)**

- Expanded series_info JSON (match details).

- Extracted Teams, Venues, Match Results.

- Merged with Team_Wins table to add logos & short names.

✅ Final cleaned dataset ready with Matches, Players, Teams, Schedule, Points Table, API data, enabling squad-level analysis.

</details>

## Data Modelling
<details>
<summary>
$\textsf{\color{blue}{View Modelling ➡️}}$
</summary> <br>

<img width="1697" height="730" alt="Image" src="https://github.com/user-attachments/assets/799c7361-1d39-43d7-83dc-0ce6212c7c60" />

**Fact Table**

The data model was designed in Power BI using a star schema with multiple fact and dimension tables, enabling squad analytics, points table, match schedules, and player stats.


- ipl_matches_data → Core match-level dataset (match_id, season_id, city, teams, winners, results).

- ball_by_ball_data → Detailed ball-by-ball records.

- bbb_bowler → Bowling stats by match.

- All_Matches_Score → Live fixture & results from API.

- 2025_batters → Batting stats for season 2025.

- 2025_bowlers → Bowling stats for season 2025.

**Relationships**

- ipl_matches_data is the central fact table, connected to:

    - Teams_data (team-level details).

    - Match_Schedule (season & venue info).

    - Players_data and Players (player-level performance).

    - Point_Table (season standings).

- 2025_captains ↔ Players (for Captain flag).

- Team_Wins ↔ Teams & Matches (logos, short names).

- Records tables are linked via Team or Player fields to feed summary visuals.

**Dimension Tables**

- Teams_data → Team details (name, short name, logo).

- Players → Player metadata (name, team, role, captain flag, image).

- 2025_captains → Captains list for 2025 squads.

- Match_Schedule → Season schedule (stadium, city, date, match_no).

- Point_Table → Standings (Matches, Wins, Losses, NRR, Points).

- Team_Wins → Team short codes and logos.

- Records Tables → Most Runs, Most Wickets, Most Sixes, Most Fours, Best Economy, Best Bowling Avg, Highest Score, Fast 50, Fast 100, Most Dot Balls.

- Highlights → Notable match records (linked with visuals).

**Supporting Tables**

- Measures → DAX calculations for KPIs.

- RefreshTable → For controlling refresh workflows.

</details>


## Data Analysis
<details>
<summary>
$\textsf{\color{blue}{Power BI: View Created Dax Measures, Columns, Tables ➡️}}$
</summary><br>

**Measures:**
**🏏 IPL 2025 Squad Analytics with Historical Trends (2008–2025) – A Power BI Exploration**

**Overview IPL KPI's**

Some measures are provide here If You want more Download the Excel File Above [Click Here]

```
Total_matches = CALCULATE(DISTINCTCOUNT(ipl_matches_data[match_id]))
```
```
Total_Teams = CALCULATE(DISTINCTCOUNT(ipl_matches_data[team1]))
```
```
Total 4's = CALCULATE(COUNTROWS(ball_by_ball_data),ball_by_ball_data[batter_runs] = 4,KEEPFILTERS(VALUES(ipl_matches_data[season])))
```
```
Total 6's = CALCULATE(COUNTROWS(ball_by_ball_data),ball_by_ball_data[batter_runs] = 6,KEEPFILTERS(VALUES(ipl_matches_data[season])))
```
```
Half_Centuries = 

VAR SelectedSeason = SELECTEDVALUE(ipl_matches_data[season])

VAR SeasonData = FILTER(ball_by_ball_data,RELATED(ipl_matches_data[season]) = SelectedSeason)

VAR BatterRuns = SUMMARIZE(SeasonData,ball_by_ball_data[match_id],ball_by_ball_data[batter], "TotalRuns" , SUM(ball_by_ball_data[batter_runs]))

VAR CenturyCount = FILTER(BatterRuns, [TotalRuns] >= 50 && [TotalRuns] <100)

RETURN COUNTROWS(CenturyCount)
```
```
Centuries = 

VAR SelectedSeason = SELECTEDVALUE(ipl_matches_data[season])

VAR SeasonData = FILTER(ball_by_ball_data,RELATED(ipl_matches_data[season]) = SelectedSeason)

VAR BatterRuns = SUMMARIZE(SeasonData,ball_by_ball_data[match_id],ball_by_ball_data[batter], "TotalRuns" , SUM(ball_by_ball_data[batter_runs]))

VAR CenturyCount = FILTER(BatterRuns, [TotalRuns] >= 100)

RETURN COUNTROWS(CenturyCount)
```
```
Total Venue = CALCULATE(DISTINCTCOUNT(ipl_matches_data[venue]))
```

</details>

## Dashboard
<details>
<summary>
$\textsf{\color{blue}{View Images ➡️}}$
</summary> <br>


> ### 1. OverView Page 

- Year Filter  – Select year to view the stats of that year.
- Profile Card – photo & stats.
- Batting Stats Card – Runs, Innings, Strike Rate, High Score, 4s, 6s.
- Bowling Stats Card – Wickets, Matches, Overs, Economy, BBI.

> <a href="https://app.powerbi.com/view?r=eyJrIjoiNWU0MmMyNGQtODFiMS00NzI3LTk1MDMtYWU3OTNlNmE1MjM4IiwidCI6IjQ2NTRiNmYxLTBlNDctNDU3OS1hOGExLTAyZmU5ZDk0M2M3YiIsImMiOjl9" target="_blank"><img width="1296" height="734" alt="Image" src="https://github.com/user-attachments/assets/24890264-f62a-4fa8-a27f-e215074ffb6c" />
</a>

> ### 2.Points Table page 

- Match Schedule – Displays matches in chronological order.
- Points Table – View team points and identify qualified teams.
- Season Filter – Slice the table & Match Schedule by season.
- Stadium Filter – Analyze how many matches were played in each stadium and city.

> <img width="1294" height="734" alt="Image" src="https://github.com/user-attachments/assets/764dd49d-c470-41f2-9ced-5b1cb45abf10" />

> ### 3. Season 2025 page 

> <img width="1306" height="737" alt="Image" src="https://github.com/user-attachments/assets/3404d63e-047b-46a9-ae4a-c3523e2fdce7" />

- Live Fixtures & Results – Track ongoing and completed matches.
- Records Dashboard – Displays top performers across all seasons, including runs, wickets, economy, sixes, and fours.
- Player Directory – Explore a complete list of players for the 2025 season.

> ### 3. Squads Of 2025 Page

><img width="1298" height="742" alt="Image" src="https://github.com/user-attachments/assets/4f44a34f-e7a1-4ec4-9fc2-2ddd9a592c8a" />

- Team Squads – View all player squads with profile images and team logos.
- Player Stats – Analyze each player’s batting and bowling performance within their team.
- Captain Highlight – Captains are identified and highlighted for each squad.
- Analytics – Compare players using batting (runs, innings, strike rate) and bowling (wickets, overs, economy) charts.

</details>


## Findings
<details>
<summary>
$\textsf{\color{blue}{View Findings ➡️}}$
</summary><br>

**📊 Tournament Summary**

- Total Matches: 74

- Total Teams: 10

- Total 4’s: 2,251

- Total 6’s: 1,296

- Half Centuries: 143

- Centuries: 9

- Venues Used: 14

**🏆 Seasons Highlights**

- Season Winner V/S Runner-up 

    - Final Result with Score Cards

**🔥 Individual Records Of all Seasons**

Example --> Season 2025:

- Orange Cap (Most Runs): **B Sai Sudharsan** – 759 runs (Gujarat Titans)

- Purple Cap (Most Wickets): **M Prasidh Krishna** – 25 wickets (Gujarat Titans)

- Most Sixes: **Nicholas Pooran** – 40 sixes (Lucknow Super Giants)

- Most Fours: **B Sai Sudharsan** – 88 fours (Gujarat Titans)

- Best Economy: **Naman Dhir** – 5.25 (Mumbai Indians)

- Most Dot Balls: **Mohammed Siraj** – 141 (Gujarat Titans)

**👑 Squad Insights**

-  Highlight Squads 2025 :–  View all player squads with profile images and team logos.

- Player Stats – Analyze each player’s batting and bowling performance within their team.

**Points Table**

Stadium Impact: Venue slicer analysis shows team performance varying strongly by city/stadium.

</details>


## Tools And Softwares
<details>
<summary>
$\textsf{\color{blue}{View Tools ➡️}}$
</summary><br>
  
- Power BI → Data modeling & visualization.
- DAX → Calculations & KPIs.
- Power Query (M) → ETL workflows.
- Excel / CSV → Player, schedule & points table data.
- CricAPI (JSON) → Live series info.
- Logos & Images → IPL Official website.

</details>
