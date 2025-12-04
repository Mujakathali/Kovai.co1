**Transit Ridership Forecasting **
**1. Objective**

The goal of this project was to analyze and forecast daily transit ridership across multiple service categories such as Local Route, Light Rail, Peak Service, Rapid Route, School, and Other. The forecasting model helps identify peak usage days, monthly trends, weekend effects, and predicts the next 7 days of ridership.

**2. Dataset Overview**

Total data points: ~2000 days

Columns included:
Date, Local Route, Light Rail, Peak Service, Rapid Route, School, Other

A new feature Total_Ridership was engineered by summing all services.

Additional temporal features: DayOfWeek, Month, Year, Quarter, IsWeekend

The dataset showed strong seasonality, especially a consistent weekly pattern where weekday ridership is higher than weekends.

**3. Key Insights From EDA**

*Highest Ridership Services:

Rapid Route recorded the highest daily riders on average.

School service showed the highest fluctuation.

*Weekend Effect:

Weekend ridership dropped by 20–40% across most services.

*Seasonality:

Clear weekly and monthly seasonality found.

Wednesday–Friday had highest usage; Saturday–Sunday sharply reduced.

*Peak & Low Months:

Highest ridership: October–November

Lowest ridership: June–July

*Correlations:

Local Route ↔ Rapid Route showed the strongest similarity in usage patterns.

**4. Modeling Approach**

I applied three types of forecasting models:

**1) ARIMA (Autoregressive Integrated Moving Average)**

Parameters selected using ACF/PACF analysis and AIC tuning.

Used differencing to achieve stationarity.

Best tuned model: ARIMA(2,1,2)

**2) SARIMA (Seasonal ARIMA)**

Incorporated weekly seasonality (period=7).

Model used: SARIMA(1,1,1)(1,1,1,7)

**3) Prophet (Meta/Facebook’s Time-Series Model)**

Automatically models trend + weekly + yearly seasonality.

Added a custom weekend regressor to improve accuracy.

Best suited for data with strong and clear seasonality (which matched our dataset).

**5. Model Performance (Compared on 30-day Test Window)**
i)Model	MAE ↓	RMSE ↓	R² ↑
ii)Prophet	5193	8219	0.07
iii)SARIMA	5958	9683	-0.28
iv)ARIMA(1,1,1)	8479	10620	-0.55
v)ARIMA(2,1,2) Tuned	8163	11215	-0.73

✓ Prophet clearly performed best with the lowest error and positive R².

Reason: Prophet is designed for datasets with strong seasonality, and our data had clear weekly patterns.

**6. Final Forecast (Using Prophet)**

Using Prophet, a 7-day forecast was generated for all service categories.
Key observations:

Predicted weekday ridership remains significantly higher than weekends.

The model successfully captured the weekday peaks and weekend troughs.

Confidence intervals were included for uncertainty estimation.

**7. Conclusion**

This project successfully built a complete end-to-end time-series forecasting pipeline:

* Data cleaning & preprocessing
* Exploratory analysis with insights
* Stationarity testing
* ARIMA & SARIMA modeling
* Hyperparameter tuning
* Prophet modeling with regressors
* Model comparison
* 7-day forecasting with visualization
