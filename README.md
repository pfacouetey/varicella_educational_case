# Varicella Time Series Forecasting

## Overview

This project predicts monthly varicella (chickenpox) case counts using time series forecasting methods. We compare classical statistical models (Holt-Winters, SARIMA) and machine learning (Random Forest) approaches on real epidemiological data (Jan 1931 – June 1972).

## Installation

### 1. Install R 4.5.1

- **Windows:**  
  Download and install from [CRAN Windows Archive](https://cran.r-project.org/bin/windows/base/old/4.5.1/)

- **Ubuntu/Debian:**
  `sudo apt-get install r-base=4.5.1`

### 2. Clone this repository and enter the project directory
 `git clone https://github.com/pfacouetey/varicella_educational_case.git`
 
 `cd varicella_educational_case`

### 3. Install and use `renv` to restore dependencies
Start R in the project directory, then run:
 `install.packages("renv")`
 
 `renv::restore()`

---

## Data

- **File:** `varicelle.csv`
- **Period:** January 1931 – June 1972
- **Frequency:** Monthly
- **Observations:** 498 monthly case counts

---

## Methods

We implement and compare the following forecasting approaches:

| Method           | Description                                      | Packages Used                  |
|------------------|--------------------------------------------------|-------------------------------|
| Holt-Winters     | Additive seasonal, damped and non-damped         | `forecast`                    |
| SARIMA           | Baseline (auto.arima) and optimized (manual ACF/PACF) | `forecast`                |
| Random Forest    | Lagged features, VSURF variable selection         | `randomForest`, `VSURF`       |

---

## Model Evaluation

- **Train/Test Split:**  
  - Training: 1931–1969  
  - Testing: 1970–1972

- **Metrics:**  
  - MAE (Mean Absolute Error)  
  - RMSE (Root Mean Squared Error)  
  - MAPE (Mean Absolute Percentage Error)

### Results

| Model                   | MAE    | RMSE   | MAPE   |
|-------------------------|--------|--------|--------|
| Holt-Winters (Damped)   | 279    | 319    | 123%   |
| SARIMA (auto.arima)     | 120    | 152    | 39%    |
| **SARIMA (Optimized)**  | **97** | **137**| **29%**|
| Random Forest           | 163    | 208    | 51%    |

- **SARIMA (optimized)** outperforms both Holt-Winters and Random Forest models on this dataset.

---

## Key Insights

- The time series shows strong **seasonality** but no clear trend.
- **SARIMA models** provide the most accurate forecasts for this epidemiological dataset.
- **Random Forest** improves on Holt-Winters but does not surpass SARIMA performance.
- Due to the limited sample size (498), model evaluation uses a fixed train/test split rather than cross-validation.

---

## Usage

1. Place `varicelle.csv` in the project root directory.
2. Open `varicelle_notebook.Rmd` in RStudio or run:
 `rmarkdown::render("varicelle_notebook.Rmd")`
3. View the results in the generated HTML notebook (`varicelle_notebook.nb.html`).

---

## Project Structure

- `varicelle_notebook.Rmd` – Main analysis notebook
- `varicelle.csv` – Data file
- `renv.lock` – Dependency lockfile for reproducible environment
- `Time-Series-Analysis.Rproj` – RStudio project file

---

## Dependency Management

All R package dependencies are managed with [renv](https://rstudio.github.io/renv/):

To initialize or update the lockfile:
`renv::init()`

`renv::snapshot()`

To restore the environment (recommended for new users):
`renv::restore()`

**Key packages:**  
- `forecast`
- `randomForest`
- `VSURF`
- `readr`

---

## Visualization

The notebook includes plots of:
- The full time series and train/test split
- Model forecasts versus actuals
- Residual diagnostics

---

## Conclusion

- **Optimized SARIMA** achieves the best performance (MAPE ≈ 29%) for forecasting monthly varicella cases.
- Machine learning (Random Forest) is promising but does not outperform the best statistical model.
- Larger datasets would allow for cross-validation and potentially further improvements.

---

## References

- Genuer, R., Poggi, J.M. & Tuleau-Malot, C. (2015). [VSURF: An R Package for Variable Selection Using Random Forests](https://journal.r-project.org/archive/2015-2/genuer-poggi-tuleaumalot.pdf). *Journal of Statistical Software*, 65(3), 1-19.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

*Educational project for time series forecasting and model comparison using epidemiological data.*



