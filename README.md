# EPL 2024-25 Player Stats: Exploratory Analysis

Exploratory analysis of Premier League player and club performance for the 2024-25 season, covering scoring, assists, appearances and discipline, with data quality checks along the way.

## Data

- **Source:** https://www.kaggle.com/datasets/aesika/english-premier-league-player-stats-2425
- **Size:** 562 players, 57 stats per player, 20 clubs, 64 nationalities
- **File:** `data/epl_player_stats_24_25.csv`

## What I looked at

- Squad size and playing time by club
- Top scorers and assist providers
- Scoring rate per 90 minutes
- Club totals for goals and assists
- Disciplinary records (yellow cards)

Scoring rate is measured per 90 minutes played, using players with at least 900 minutes so that small samples don't dominate the rankings:

$$\text{goals per 90} = \frac{\text{Goals}}{\text{Minutes}} \times 90$$

## Key findings

- **Mohamed Salah led the league in both goals (29) and assists (18).** Alexander Isak (23) and Erling Haaland (22) were next in goals.
- **Salah also had the highest scoring rate** among players with 900+ minutes, at about 0.77 goals per 90.
- **Squad stability varied a lot.** Nottingham Forest players averaged the most appearances (about 25.5 each), while Southampton players averaged the fewest (about 16.8) and used the most players overall (34).
- **Most players had less than 25 appearances.** Exactly 58.3% had 25 apperances or less and 47.2% with less than 20

## Data quality

I validated the dataset before trusting it, and found several problems:

- **Missing goals.** Player goals sum to 963, but the real season total was 1,115. Most clubs are within a few goals of their official total (opponents' own goals aren't credited to any player), but some, notably Liverpool and Bournemouth, are well short. Club-level goal totals should be read with this in mind.
- **Shots On Target is unreliable per player.** Many players have more goals than shots on target, which is impossible (for example, 7 of 30 Brighton players). I use this column only in league-wide totals, not for per-player accuracy.
- **Naming inconsistency.** Brighton appeared under two spellings, which split the club's players into two groups. I merged them.
- **Percent columns were stored as text** (e.g. `"72%"`) and converted to numbers.

Player-level goal and assist rankings match the real season, so I treat those as reliable.

## How to run

```bash
git clone https://github.com/pavito157/EPL24_25_AnalysisDemo.git
cd EPL24_25_AnalysisDemo
pip install -r requirements.txt
jupyter notebook
```

Then open the notebook and run all cells.

## Tools

Python, pandas, NumPy, matplotlib, seaborn, Jupyter

## Next steps

Planned: goalkeeper analysis (saves, goals prevented) and ball-carrying (progressive carries, dispossessions), per 90 minutes.
