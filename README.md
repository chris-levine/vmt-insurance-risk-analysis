# Forecasting Vehicle Miles Traveled as a Proxy for Auto Insurance Exposure

## Overview

This project analyzes whether macroeconomic variables can improve forecasts of **Vehicle Miles Traveled (VMT)**, a proxy for aggregate driving exposure. In the context of auto insurance, driving exposure matters because more miles driven generally creates more opportunities for accidents and claims.

Because direct auto insurance claim count data is often proprietary and difficult to access publicly, this project uses VMT as a practical proxy for exposure to auto insurance risk. The goal is to forecast monthly VMT growth and evaluate whether macroeconomic information improves predictive accuracy compared to simple benchmark forecasting models.

The analysis uses monthly U.S. data from **January 2000 to February 2026** and compares five forecasting approaches:

- Naive mean model
- Random walk model
- Random walk with drift model
- Full macroeconomic regression model
- Principal Component Analysis (PCA) factor model

Forecasts are evaluated at both **one-month-ahead** and **twelve-month-ahead** horizons using an expanding-window forecasting framework.

## Research Question

Can macroeconomic information improve forecasts of Vehicle Miles Traveled growth compared to simple benchmark forecasting models?

More specifically, does a PCA-based factor model improve forecast accuracy by summarizing macroeconomic variables into a smaller number of latent factors?

## Why This Matters

Vehicle Miles Traveled is closely related to auto insurance exposure. While it does not directly measure claim counts, changes in driving activity can help inform discussions about:

- Claim frequency risk
- Auto insurance exposure
- Underwriting conditions
- Insurance pricing considerations
- Broader transportation and macroeconomic trends

This project demonstrates how time series forecasting and macroeconomic modeling can be applied to an insurance-related risk problem.

## Data

The dataset uses monthly U.S. time series from the Federal Reserve Economic Data (FRED) database.

### Dependent Variable

- **Vehicle Miles Traveled (VMT)** — proxy for aggregate driving exposure

### Predictor Variables

- Gas prices
- Auto sales
- Unemployment rate
- Consumer Price Index (CPI)
- Industrial production
- Federal funds rate

The sample period runs from **January 2000 to February 2026**. Weekly gas price data was converted to monthly frequency by averaging observations within each month. Intermittent missing values were filled using the previous month’s observed value to maintain a continuous time series.

## Methods

### 1. Stationarity Testing and Transformations

Before estimating forecasting models, the time series were tested for stationarity using:

- Autocorrelation and partial autocorrelation plots
- Augmented Dickey-Fuller tests

Non-stationary variables were transformed using log differences to convert them into monthly growth rates. This step reduces the risk of spurious regression and makes the data more appropriate for forecasting.

Variables transformed using log differences included:

- VMT
- Gas prices
- CPI
- Industrial production

Variables kept in levels included:

- Auto sales
- Unemployment rate
- Federal funds rate

### 2. Benchmark Forecasting Models

Three simple benchmark models were used as baselines:

- **Naive mean model:** Forecasts future VMT growth using the historical average.
- **Random walk model:** Forecasts the next value using the current value.
- **Random walk with drift:** Adds an average change term to the random walk model.

These benchmarks are important because simple forecasting models are often difficult to outperform in economic time series.

### 3. Full Macroeconomic Regression Model

A full regression model was estimated using lagged VMT growth and lagged macroeconomic predictors. Monthly dummy variables were included to account for seasonality.

This model tests whether directly including macroeconomic variables improves VMT growth forecasts.

### 4. PCA Factor Model

Principal Component Analysis was used to reduce the macroeconomic predictors into a smaller number of uncorrelated latent factors.

The PCA factor model includes:

- Lagged VMT growth
- Lagged PCA factors
- Monthly seasonal dummy variables

This approach tests whether summarizing macroeconomic information through latent factors improves forecast accuracy compared to using the full set of macroeconomic variables directly.

### 5. Forecast Evaluation

Each model was evaluated using an expanding-window forecasting approach. Forecasts were generated at:

- **h = 1:** one-month-ahead forecasts
- **h = 12:** twelve-month-ahead forecasts

Forecast accuracy was measured using:

- **Mean Squared Forecast Error (MSFE)**
- **Mean Absolute Error (MAE)**

Lower MSFE and MAE values indicate better forecast performance.

## Key Results

The naive mean model produced the strongest overall forecast performance at both the one-month and twelve-month forecast horizons.

At the one-month horizon, the naive mean model achieved:

- **MSFE:** 0.002574
- **MAE:** 0.019261

At the twelve-month horizon, the naive mean model achieved:

- **MSFE:** 0.002924
- **MAE:** 0.020793

Although the PCA factor model did not outperform the naive mean model, it was the strongest model among the more complex approaches. It consistently outperformed the random walk, random walk with drift, and full macroeconomic regression models.

This suggests that while simple historical averages were most effective for forecasting monthly VMT growth, PCA may still be useful for summarizing macroeconomic conditions and improving upon direct macroeconomic regression approaches.

## Robustness Check

A robustness check was performed by changing the initial training period from **January 2000–December 2018** to **January 2000–December 2015**.

The results remained consistent:

- The naive mean model remained the strongest overall forecasting model.
- The PCA factor model remained the strongest complex model.
- The full macroeconomic regression model did not outperform the PCA factor model.

This supports the stability of the main findings.

## Main Takeaways

- Vehicle Miles Traveled can be used as a proxy for aggregate auto insurance exposure.
- Monthly VMT growth is difficult to forecast using macroeconomic predictors.
- The naive mean model produced the lowest forecast errors overall.
- PCA outperformed the full macroeconomic regression model, suggesting that dimension reduction can improve forecasting performance when using macroeconomic predictors.
- More complex models do not automatically produce better forecasts, especially when simple benchmark models capture the key behavior of the series.

## Limitations

This project uses VMT as a proxy for auto insurance claim exposure, not direct claim count data. Actual insurance claim data would provide a more direct measure of claim frequency risk, but such data is often proprietary.

The COVID-19 period also created an unusually large shock to driving activity, which may have affected model performance. Future work could include additional robustness checks or explicit controls for the COVID-19 shock.

## Future Improvements

Possible extensions of this project include:

- Adding COVID-19 shock controls
- Testing additional forecasting models such as ARIMA, VAR, or machine learning models
- Using actual claim frequency data if available
- Comparing state-level or regional VMT patterns
- Incorporating additional insurance-related variables such as accident rates, fuel consumption, or policy exposure data

## Files

- `paper/forecasting-vmt-insurance-exposure-paper.pdf` — Full written research paper
- `notebooks/` — Code and analysis notebooks
- `data/` — Raw or processed data files, if included
- `visuals/` — Forecast plots, PCA visualizations, and supporting charts

## Skills Demonstrated

- Time series forecasting
- Principal Component Analysis
- Macroeconomic data analysis
- Forecast evaluation
- Stationarity testing
- Data transformation
- Statistical modeling
- Insurance exposure analysis
- Research writing
- Python / R data analysis

## Citation

Data used in this project was sourced from the Federal Reserve Economic Data (FRED) database, including series from the Federal Reserve Bank of St. Louis, the U.S. Bureau of Transportation Statistics, the U.S. Bureau of Labor Statistics, the U.S. Energy Information Administration, and the U.S. Bureau of Economic Analysis.
