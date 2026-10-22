# ab-testing

A/B test analysis on the Cookie Cats mobile game dataset: does moving the first forced-wait gate from level 30 to level 40 change whether players come back?

## What's in here

- `cookie_cats_ab_test.ipynb` - the full analysis, runs top to bottom
- `requirements.txt`

## Data

Cookie Cats A/B test data: 90,189 players, randomly shown the first gate at level 30 (`gate_30`) or level 40 (`gate_40`), with 1-day and 7-day retention flags and rounds played in the first 14 days.

Source: [Mobile Games A/B Testing - Cookie Cats on Kaggle](https://www.kaggle.com/datasets/mursideyarkin/mobile-games-ab-testing-cookie-cats) (data from Tactile Entertainment). The notebook downloads the CSV itself on first run (from [this mirror](https://github.com/ryanschaub/Mobile-Games-A-B-Testing-with-Cookie-Cats)) and saves a copy to `data/`. You can also drop `cookie_cats.csv` into `data/` yourself.

## What I did

- set the question, metrics and decision rule before touching any numbers
- audited the data: types, missing values, duplicate users, group sizes, round-count outliers
- retention rates with Wilson confidence intervals, plus absolute and relative effect size
- two-proportion z-test with a chi-square cross-check, Holm correction for the two metrics
- sample ratio mismatch check on the randomization split
- bootstrap check that makes no normality assumption
- power analysis: smallest detectable effect at this sample size and the n you'd actually need
- engagement segments to see whether one slice of players carries the result

## Result

Keep the gate at level 30. Day-7 retention is about 0.8 percentage points lower with the gate at level 40 (19.0% vs 18.2%, p = 0.0016, and the bootstrap agrees). Day-1 retention moves the same way but isn't conclusive on its own. At this scale that's roughly 740 players lost per 90k installs. One caveat: the group split isn't exactly 50:50 and a chi-square check flags it, so there's a small unresolved question about the randomization (details in the notebook).

## Run it

```
pip install -r requirements.txt
jupyter notebook cookie_cats_ab_test.ipynb
```
