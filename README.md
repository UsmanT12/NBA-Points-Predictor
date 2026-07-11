# NBA Player Points Prediction

This project predicts an NBA player's points in their next game using recent form, playing time, shooting volume, matchup context, rest, and player archetype. It compares a rolling-average baseline with linear regression, random forest, and XGBoost models.

## Project overview

The analysis follows a time-aware machine-learning workflow:

1. Clean game-level player statistics and retain rotation players.
2. Explore scoring distributions, playing time, shot volume, matchups, and recent form.
3. Engineer lagged rolling statistics, efficiency measures, rest indicators, opponent features, and player archetypes.
4. Reduce multicollinearity with correlation and variance inflation factor (VIF) filtering.
5. Use a chronological 80/20 train-test split to avoid training on future games.
6. Compare a five-game rolling baseline, linear regression, random forest, and tuned XGBoost.

## Results

The saved notebook run produced the following test-set results:

| Model | RMSE | MAE | R² |
| --- | ---: | ---: | ---: |
| 5-game rolling baseline | 7.090 | 5.522 | 0.309 |
| Linear regression | 5.813 | 4.520 | 0.536 |
| Random forest | **5.805** | **4.514** | **0.537** |
| XGBoost | 6.017 | 4.663 | 0.503 |

Linear regression and random forest performed almost identically on unseen games. Random forest achieved the best overall test RMSE, MAE, and R², while XGBoost showed a larger train-test gap.

## Repository structure

```text
nba-player-points-prediction/
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   └── nba_points_prediction.ipynb
├── docs/
│   └── NBA_Points_Prediction.pdf
└── data/
    └── README.md
```

The image files are intentionally left for the final notebook exports.

## Setup

Clone the repository and create a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Download the source dataset as described in [`data/README.md`](data/README.md), then place it at:

```text
data/PlayerStatistics.csv
```

Start Jupyter and run the notebook from top to bottom:

```bash
jupyter lab notebooks/nba_points_prediction.ipynb
```

## Notes

- Rolling features are shifted by one game so a target game's result is not used to predict itself.
- The train-test split is chronological rather than randomized.
- The dataset is excluded from Git because of its size.
- Results may change when the source data is updated or the models are retrained.

## Project report

The accompanying presentation is available at [`docs/NBA_Points_Prediction.pdf`](docs/NBA_Points_Prediction.pdf).
