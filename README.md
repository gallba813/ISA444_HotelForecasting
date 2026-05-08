# ISA 444 — Hotel Demand Forecasting
**Farmer School of Business | Miami University**

Author: Boden Gall

## Project Overview
This project forecasts daily room occupancy rates for 19 hotel properties over a 28-day horizon using 5-fold non-overlapping time-series cross-validation. Eight models were compared across four evaluation metrics: bias (ME), MAE, RMSE, and MAPE.

## Models Compared
| Family | Models |
|--------|--------|
| Baseline | Naive, Seasonal Naive |
| Statistical | AutoETS, AutoARIMA |
| Machine Learning | LightGBM |
| Neural | NBEATS, NHITS |
| Foundation | Chronos (amazon/chronos-bolt-small) |

## Repository Contents
| File | Description |
|------|-------------|
| `isa444_FinalProject.ipynb` | Full modeling pipeline |
| `cv_evaluation_results.csv` | Cross-validation metrics by series and model |
| `model_win_counts.csv` | Count of wins per model per metric |
| `final_forecasts_statsforecast.csv` | Final forecasts — Naive, SeasonalNaive, AutoETS, AutoARIMA |
| `final_forecasts_lightgbm.csv` | Final forecasts — LightGBM |
| `final_forecasts_neural.csv` | Final forecasts — NBEATS, NHITS |
| `final_forecasts_chronos.csv` | Final forecasts — Chronos |
| `forecast_plot_*.png` | Forecast vs actual plots for each hotel |

## Key Findings
Chronos was the strongest overall performer, winning the most series on MAE (8 wins), MAPE (8 wins), and RMSE (7 wins). This is notable given that Chronos is a zero-shot foundation model with no hotel-specific training, demonstrating strong generalization capability. LightGBM was the second strongest model, performing well across all metrics by leveraging lag-based features and day-of-week patterns. AutoETS and AutoARIMA were competitive on statistical metrics, particularly for hotels with stable occupancy patterns such as airport and CBD properties. NBEATS and NHITS showed moderate performance, while Naive and SeasonalNaive were the weakest overall.

Performance varied meaningfully across series. Hotels with stable, high-occupancy patterns tended to be easier to forecast across all models, while leisure and resort properties showed higher error, likely due to greater demand volatility around holidays and seasonal peaks. Hotel 77 had a shorter and gapped series which required preprocessing before modeling.

MAPE should be interpreted with caution for this dataset. The occupancy target contains zero values which cause division by zero and inflate MAPE for low-occupancy periods. MAE and RMSE are the more reliable metrics for comparing model performance.

## Packages Used
- `statsforecast` — Naive, SeasonalNaive, AutoETS, AutoARIMA
- `mlforecast` — LightGBM
- `neuralforecast` — NBEATS, NHITS
- `timecopilot` — Chronos
- `utilsforecast` — Evaluation metrics
