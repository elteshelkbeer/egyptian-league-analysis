# Egyptian Premier League vs the World: 10 Seasons of Data (2015-2025)

Exploratory data analysis of 2,907 Egyptian Premier League matches across 10 seasons,
compared with 3,800 English Premier League and 2,358 Saudi Pro League matches over the
same span, using Python, pandas, matplotlib and seaborn. My first portfolio project as a
junior data analyst.

## Questions this project answers

1. How many goals does the Egyptian league score, and is that changing over time?
2. Does playing at home really help in Egypt - and why/why not, club by club?
3. Who actually dominates the league? (I rebuild the standings table from raw match results)
4. Who are the best scorers of the decade?
5. Which team had the best defense?
6. How close are the matches?
7. Egypt vs England over the same 10 seasons: what is actually different?
8. The fan-power test: does Saudi Arabia - where fans fill their clubs' own stadiums -
   look like Egypt or like England?

## Headline findings

**Egyptian league (2,907 matches):**

- **Al Ahly won 7 of the 9 completed league titles** (2015-16 through 2023-24) and win
  **72.4%** of all their league matches across the decade. Zamalek won the other 2 titles
  (2020-21, 2021-22) at a 59.1% win rate.
- **Home advantage barely exists at league level:** home teams win only **36.5%** of matches
  vs **30.8%** for away teams (England: 44.5/32.2). But the league average hides the real
  story - see the club-by-club finding below.
- **Al Ahly's 2019-20 defense conceded 8 goals in 34 matches** (a clean sheet in 28 of 34),
  the single most extreme stat in the dataset. They also lead the decade with **187 clean
  sheets**; the best non-Ahly team has 140.
- **The league is low-scoring and tight:** 2.29 goals per match on average (flat across 10
  seasons), **73.1%** of matches are decided by at most one goal, the most common result is
  1-1 (412 matches), and **12.3%** of matches end 0-0.
- **Abdallah El Said is the top scorer of the decade** with 76 goals (own goals removed),
  ahead of Hossam Hassan (69) and Zizo (61). Identity check (notebook section 5): the raw
  data merges namesakes, so 8 "Hossam Hassan" goals at El Sharkia (a different player, a
  defensive midfielder) and 12 "Zizo" goals at El Dakhlia (the Zamalek star was in Europe
  then) were split out. The Hossam Hassan here is the Smouha/Al Ittihad striker born in
  1993, not the 1966 legend - and his 69 goals match his documented career exactly.

**Home advantage is a club-by-club story:**

- **El Masry is the extreme case:** over 10 seasons they played "home" matches in **8
  different stadiums, none of them in Port Said** - their most-used "home" ground is Borg El
  Arab Stadium *in Alexandria, another city* (91 of 161 matches). Their home win rate (39.8%)
  is *lower* than their away win rate (41.4%): a negative home advantage. (Context, not from
  the dataset: Port Said clubs were banned from playing at home for years after the 2012
  Port Said stadium disaster.)
- **Wadi Degla (-5.9) and Entag El Harby (-2.5)**, Cairo clubs that rent mega-venues, also
  have negative home advantage.
- **Provincial clubs with one true home ground show the normal pattern:** Aswan +14.8,
  El Gouna +13.1, Pharco +13.0, Petrojet +12.7, El Mahalla +12.0 (home win% minus away
  win%), averaging +8.1. The advantage exists in Egypt - only where a real home does.
- Scale of venue sharing: the average club used **5.1 different "home" stadiums** over the
  decade, and the top 3 mega-venues (Petrosport, Borg El Arab, Cairo International) host
  **32.8%** of all matches.

**Egypt vs England, same 10 seasons (3,800 EPL matches):**

- England scores more: **2.83 vs 2.29 goals per match**, every single season - and England
  is trending up (a record 3.28 in 2023-24) while Egypt stays flat.
- Home advantage: **44.5% vs 36.5%** home wins; draws **23.3% vs 32.7%**; 0-0 draws are
  twice as common in Egypt (**12.3% vs 6.2%**).
- **COVID killed home advantage in both leagues:** in empty-stadium 2020-21, England's
  home-win rate crashed from 45.3% to 37.9% (below the 40.3% away rate) and Egypt's fell to
  31.0% (below 32.4% away) - the cleanest proof in the data that crowds are the advantage.
- Different kinds of imbalance: England has the bigger top-to-bottom points gap (71 vs 61
  on average), but Egypt had only **2 champions in 9 completed seasons vs 4 in England**
  (Man City 5, Liverpool, Chelsea, Leicester).
- Penalties: **15.3% of Egyptian goals vs 7.7% of English goals** (2015-2023, the span the
  EPL goal-level data covers).

**The fan-power test: Saudi Arabia as the control group (2,358 matches):**

- **Saudi Arabia looks like England, not like Egypt** - same region and football culture as
  Egypt, but with fans in their clubs' own stadiums: goals per match **2.90** (England 2.83,
  Egypt 2.29), home wins **43.5%** (44.5%, 36.5%), draws **23.5%** (23.3%, 32.7%), 0-0 draws
  **6.0%** (6.2%, 12.3%).
- **The stands:** England averages ~40,000 per match; Saudi Arabia ~8,000 league-wide but
  **22,461 for its big 4 popular clubs vs 4,325 for the rest** (2024-25). Egyptian clubs,
  by contrast, played with no crowds at all for 6.5 years after 2012 and are still capped at
  20,000 per match (regulatory caps from news reports, not dataset findings).
- **A stadium of one's own:** 18 Saudi clubs play in 15 stadiums (only city-mates share) and
  20 English clubs in 20 - while Egyptian clubs used 5.1 stadiums each. Champions in the
  decade: **2 in Egypt, 4 in Saudi Arabia, 4 in England**.

## How to run

```bash
pip install pandas matplotlib seaborn jupyter
jupyter notebook egyptian_premier_league_analysis.ipynb
```

Run the cells top to bottom. The notebook reads the CSVs in `data/` (already included),
so it works offline.

## Data sources and licenses

**Egyptian league:** [10 Seasons Egyptian League](https://www.kaggle.com/datasets/ahmedaelgohary/10-seasons-egyptian-league)
by Ahmed Elgohary on Kaggle, compiled from a football statistics website.
License: **Open Database License (ODbL) / Database Contents License** - used with attribution.

- `result_combined.csv` - one row per match: date, teams, score, result (2,907 matches)
- `goals_combined.csv` - one row per goal: scorer, own-goal flag, assist, penalty flag (6,635 goals)
- `refandstadium_combined.csv` - referee and stadium per match

**English league (match results):** [football-data.co.uk](https://www.football-data.co.uk/data.php)
season CSVs (free for personal/educational use), combined into `epl_results.csv`
(3,800 matches, 2015-16 to 2024-25).

**English league (goal-level, for the penalty comparison):**
[Football - 10 years of EPL with goal timing](https://www.kaggle.com/datasets/nico2890/football-10-years-of-epl-with-goal-timing)
on Kaggle (license not stated on the dataset page; used here with attribution), filtered to
2015-16 to 2022-23 in `epl_goals_2015_2023.csv`. Cross-check: its 8,393 goals match the
football-data results exactly for the same span.

**Saudi league (match results + attendance):** results grids and league-published attendance
tables from the 10 Wikipedia season pages (e.g.
[2024-25 Saudi Pro League](https://en.wikipedia.org/wiki/2024%E2%80%9325_Saudi_Pro_League)),
license **CC BY-SA 4.0**, parsed into `spl_results.csv` (2,358 matches) and
`spl_attendance.csv`. Verification: match counts exact for all 10 seasons; 845 of 846 scores
identical to ESPN's data for the 3 seasons ESPN covers (the one difference is an officially
awarded match, kept as awarded); champions computed from the data match official history
all 10 seasons.

**Egypt crowd context (not data):** [BBC (2018)](https://www.bbc.com/sport/football/45185133),
[The Guardian (2018)](https://www.theguardian.com/football/2018/sep/12/port-said-riot-egypt-football-fans-stadiums),
[Ahram Online (2024)](https://english.ahram.org.eg/NewsContent/6/51/517938/Sports/Egyptian-Football/Egyptian-Premier-League-doubles-attendance-to-,.aspx).
England/Saudi measured attendance from the Wikipedia season pages above plus the
[Premier League season pages](https://en.wikipedia.org/wiki/2024%E2%80%9325_Premier_League).

## Caveats (found during data cleaning)

- Egyptian season 2024-25 is **partial**: 153 matches up to 5 March 2025 (the Kaggle page
  says 29 April, but the latest match in the files is 5 March), so it is excluded
  from season totals and the champions analysis (per-match rates still use it).
- The Egyptian goals table has 10 goals fewer than the results imply (6,635 vs 6,645, 0.15%).
  Scorer rankings are unaffected at the top.
- Scorers are merged by exact name, which merges namesakes: verified the top 10 club-by-club
  and split out 20 goals belonging to two different players (see notebook section 5).
- The 2015-2025 window bounds career totals. Example: striker Hossam Hassan's full league
  record is 77 goals, but 2 pre-date the window (El Gaish, El Dakhleya) and 6 post-date it
  (Modern Sport, Al Ittihad), so this project credits him with the 69 scored inside it.
- 24 Egyptian matches (0.8%) have no stadium/referee info; the rest of the stadium table
  covers all 10 seasons.
- EPL goal-level data ends at 2022-23, so the penalty comparison uses 2015-2023 on both sides.
- Kick-off time is missing for 455 Egyptian matches; not used in any analysis.
- Team names are as written in the datasets: `Ahly SC` = Al Ahly, `El Masry` = Al Masry.
- Attendance figures exist in neither the Egyptian nor the English match datasets, so
  fan-restriction context is labeled as history, not as something the data proves. What the
  data does prove is the COVID empty-stadium collapse of home advantage. Saudi and English
  measured attendance come from league-published figures via Wikipedia (no 2020-21 figures,
  COVID); Egypt publishes no attendance, only government crowd caps.
- One Saudi match was decided off the pitch: Al-Orobah 0-3 Al-Nassr (28 Feb 2025) ended 0-0
  and was awarded to Al-Nassr by the Saudi Sports Arbitration Centre (ineligible player);
  the official awarded result is kept, matching Wikipedia.
- The Saudi file has no goal scorers, so scorer/penalty analyses stay Egypt-vs-England.

## Project structure

```
egyptian-league-analysis/
├── egyptian_premier_league_analysis.ipynb   # the full analysis, all charts included
├── data/                                    # the 8 CSVs (3 Egyptian + 3 English + 2 Saudi)
└── README.md
```
