# PM10 Air Quality Classification ☁️

Binary classification of PM10 air pollution exceedances using machine learning methods in R

## Project Overview 📖

This project predicts whether hourly PM10 particulate matter concentrations will exceed
the EU air quality standard of **50 µg/m³**, based on meteorological and traffic data
collected in Oslo, Norway.

Two models are compared:
- **Random Forest** — ensemble method with asymmetric class weights
- **CART** — interpretable decision tree with asymmetric loss matrix

## Dataset 🗂️

**Source:** Norwegian Public Roads Administration — Alnabru, Oslo, Norway (Oct 2001 – Aug 2003)  
**Size:** 500 hourly observations · 8 features · no missing values  
**Contact:** Magne Aldrin (magne.aldrin@nr.no)

| Feature | Description |
|---|---|
| `log_PM10` | ln(PM10 concentration) — target variable |
| `log_cars` | ln(hourly traffic volume) |
| `temp_2m` | Air temperature at 2m (°C) |
| `wind_speed` | Wind speed (m/s) |
| `tempdiff_25_2m` | Temperature diff. 25m vs 2m — atmospheric stability proxy |
| `wind_dir` | Wind direction (0–360°) |
| `hour` | Hour of measurement (1–24) |
| `dayno` | Day number from October 1, 2001 |

**Class balance:** `norm` 77.2% / `exceed` 22.8%
## Results Summary 📊

| Metric | Random Forest | CART |
|---|---|---|
| Recall (Sensitivity) | **0.71** | 0.61 |
| Specificity | 0.77 | **0.82** |
| Balanced Accuracy | **0.74** | 0.71 |
| Precision (`exceed`) | — | 0.50 |

**Confusion Matrix — Random Forest**

|  | Predicted: norm | Predicted: exceed |
|---|---|---|
| **Actual: norm** | 73 | 22 |
| **Actual: exceed** | 8 | 20 |

**Confusion Matrix — CART**

|  | Predicted: norm | Predicted: exceed |
|---|---|---|
| **Actual: norm** | 78 | 17 |
| **Actual: exceed** | 11 | 17 |

## Key Findings 🔍

- **Most important feature** in both models: `tempdiff_25_2m` (atmospheric stability)
- High importance also for: `log_cars` (traffic volume) and `wind_dir` (wind direction)
- **Random Forest outperforms CART** in detecting exceedances (Recall 0.71 vs 0.61),
  making it better suited for air quality monitoring where missing a true exceedance
  is more costly than a false alarm
- CART offers higher interpretability through explicit decision rules visible in the tree plot

## Requirements ✔️
```r
install.packages(c("caret", "randomForest", "rpart", "rpart.plot", "ggplot2"))
```
## Usage

> ⚠️ Update the file path in the first code chunk of the `.Rmd` file to match your local `PM10.dat` location before knitting.
