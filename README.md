# Egyptian Premier League vs the World: 10 Seasons of Data (2015-2025)

Exploratory data analysis of 2,907 Egyptian Premier League matches across 10 seasons,
compared with 3,800 English Premier League matches over the same span, using Python,
pandas, matplotlib and seaborn. My first portfolio project as a junior data analyst.

## Questions this project answers

1. How many goals does the Egyptian league score, and is that changing over time?
2. Does playing at home really help in Egypt - and why/why not, club by club?
3. Who actually dominates the league? (I rebuild the standings table from raw match results)
4. Who are the best scorers of the decade?
5. Which team had the best defense?
6. How close are the matches?
7. Egypt vs England over the same 10 seasons: what is actually different?

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
- **Hossam Hassan is the top scorer of the decade** with 77 goals (own goals removed),
  ahead of Abdallah El Said (76) and Zizo (73).

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
- Penalties: **15.4% of Egyptian goals vs 7.7% of English goals** (2015-2023, the span the
  EPL goal-level data covers).

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

## Caveats (found during data cleaning)

- Egyptian season 2024-25 is **partial**: 153 matches up to 29 April 2025, so it is excluded
  from season totals and the champions analysis (per-match rates still use it).
- The Egyptian goals table has 10 goals fewer than the results imply (6,635 vs 6,645, 0.15%).
  Scorer rankings are unaffected at the top.
- 24 Egyptian matches (0.8%) have no stadium/referee info; the rest of the stadium table
  covers all 10 seasons.
- EPL goal-level data ends at 2022-23, so the penalty comparison uses 2015-2023 on both sides.
- Kick-off time is missing for 455 Egyptian matches; not used in any analysis.
- Team names are as written in the datasets: `Ahly SC` = Al Ahly, `El Masry` = Al Masry.
- Attendance figures exist in neither dataset, so fan-restriction context is labeled as
  history, not as something the data proves. What the data does prove is the COVID
  empty-stadium collapse of home advantage in both leagues.

## Project structure

```
egyptian-league-analysis/
├── egyptian_premier_league_analysis.ipynb   # the full analysis, all charts included
├── data/                                    # the 5 CSVs (3 Egyptian + 2 English)
└── README.md
```
