# German Stock Market Returns | Time Series Forecasting

**Academic group project · Financial time series · Econometrics · Deep learning**

## Project overview
This project investigated whether macroeconomic indicators improve forecasts of **German stock market returns**. We compared two classical econometric approaches, **SARIMAX** and **Vector Autoregression (VAR)**, with a recurrent neural network, **Gated Recurrent Unit (GRU)**.

The study examined three monthly time series obtained from **Federal Reserve Economic Data (FRED)**:
- **German stock share-price index**, the forecasting target.
- **Real Effective Exchange Rate (REER)** for Germany.
- **Economic Policy Uncertainty (EPU)** index for Germany.

The common study period was **January 1994 to March 2026**, with **387 monthly observations** in levels and **386 after transformation**.

This was an **academic group project**. Collaborators' names and student identifiers are not published here.

## Research questions
1. Do exchange-rate movements and economic policy uncertainty contain statistically significant predictive information for German stock returns?
2. Which forecasting model performs best out of sample?
3. Does a nonlinear GRU model outperform traditional econometric approaches?

## Data preparation and exploratory analysis
- Retrieved the three FRED series, aligned their monthly time indexes and checked missing values.
- Explored distributions, time trends, seasonality and **autocorrelation / partial autocorrelation (ACF and PACF)**.
- Transformed REER and EPU into **log returns** to address nonstationarity. The stock-price series used for modelling was already expressed as monthly growth.
- Applied **Augmented Dickey-Fuller (ADF)**, **Phillips-Perron (PP)** and **KPSS** stationarity tests.
- Used a chronological **90% training / 10% testing split**, rather than random shuffling, to preserve temporal order.

## Models and methodology

### SARIMAX
- Selected a **SARIMAX(1,0,0)** specification through stepwise auto-ARIMA using **AIC**.
- Used one-period-lagged REER and EPU returns as exogenous regressors to avoid contemporaneous information leakage.
- Evaluated residual diagnostics and out-of-sample forecasts.

### Vector Autoregression (VAR)
- Modelled stock, REER and EPU returns jointly as endogenous time series.
- Compared lag-order criteria including **AIC, BIC and HQIC**; selected a parsimonious **VAR(1)**.
- Investigated dynamic relationships using **Granger causality** and cointegration tests.
- Estimated the model on stationary series rather than using VECM because the variables had different integration orders.

### Gated Recurrent Unit (GRU)
- Implemented a recurrent neural network with a **three-month input window**, **32 hidden units** and a dense output layer.
- Applied **MinMaxScaler fitted on the training data only** to reduce leakage.
- Used **RMSprop**, **mean squared error (MSE)** and **early stopping** to limit overfitting.

## Model evaluation
Models were compared using **Root Mean Squared Error (RMSE)**, **Mean Absolute Error (MAE)** and **Directional Accuracy (DA)** on the held-out test period.

| Model | RMSE | MAE | Directional accuracy |
| --- | ---: | ---: | ---: |
| SARIMAX | 3.504 | 2.741 | 56.41% |
| **VAR(1)** | **3.415** | **2.700** | **59.00%** |
| GRU | 3.842 | 3.082 | 59.00% |

**VAR(1)** achieved the lowest RMSE and MAE and matched the GRU's directional accuracy. The additional complexity of the GRU did not translate into a forecasting advantage in this experiment.

## Statistical findings and interpretation
The reported Granger causality tests did **not** find evidence that REER or EPU significantly improved forecasts of German stock returns. The report did identify a significant relationship in the reverse direction: stock returns helping predict economic policy uncertainty.

Overall, the models had relatively similar performance and limited predictive ability. These findings were discussed in relation to the **Efficient Market Hypothesis**, without claiming that the study proves the hypothesis.

## Technical skills demonstrated
**Python · pandas · NumPy · FRED data access · statsmodels · SARIMAX · VAR · Granger causality · ADF / PP / KPSS · TensorFlow / Keras · GRU · scikit-learn · Time-series validation · Forecast evaluation**

## Full project access
> **Full project available upon request.** The complete analysis notebook and academic report are retained privately. Only this technical case study is publicly shared.

*This is a group academic exercise, not financial advice or a production trading model.*
