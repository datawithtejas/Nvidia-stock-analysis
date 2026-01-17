# NVIDIA Stock Performance & Volatility Analysis

## Project Overview
This project conducts a rigorous statistical analysis of NVIDIA Corporation's (NVDA) stock performance. Leveraging Python and the `statsmodels` library, the analysis models the relationship between market indicators and stock price behavior. The primary goal is not just prediction, but ensuring statistical validity through extensive diagnostic testing of the Ordinary Least Squares (OLS) regression model.

## Key Methodology
* **Data Acquisition:** Automated retrieval of historical market data.
* **OLS Regression Modeling:** Built linear models to quantify the impact of trading volume and moving averages on stock returns.
* **Advanced Diagnostic Checks:**
    * **"Four-in-One" Visual Diagnostics:** Implemented a custom 2x2 grid (Residuals vs. Fitted, Normal Q-Q, Scale-Location, Residuals vs. Leverage) to validate assumptions of linearity and homoscedasticity.
    * **Multicollinearity Detection:** Calculated **Variance Inflation Factors (VIF)** to identify and remove redundant predictors.
    * **Autocorrelation Testing:** Applied the **Durbin-Watson statistic** to detect serial correlation in time-series residuals.
    * **Normality Verification:** Used histograms and Q-Q plots to ensure residual normality.

## Technologies Used
* **Python:** Core analysis and scripting.
* **Statsmodels:** Advanced statistical modeling and testing (OLS, VIF).
* **Matplotlib & Seaborn:** Custom diagnostic plotting and data visualization.
* **Pandas & NumPy:** Data manipulation and vectorization.

## Key Insights
* *Verified model assumptions using a custom diagnostic pipeline.*
* *Identified key influential data points (outliers) using Leverage plots.*
