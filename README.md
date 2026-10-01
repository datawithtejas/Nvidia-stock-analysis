Plaintext# NVIDIA Stock Return & Sentiment Analysis

## Project Overview
This project conducts an empirical econometric analysis of NVIDIA Corporation’s (NVDA) daily stock returns. Utilizing Python and the `statsmodels` framework, the project tests whether daily stock returns can be predicted using 1-day lagged moves from key semiconductor supply chain partners—Taiwan Semiconductor Manufacturing Company (TSM) and ASML Holding (ASML)—alongside daily news sentiment scores. 

The core focus is investigating market efficiency, supply-chain lead/lag dynamics, and the relative impact of qualitative market sentiment versus quantitative manufacturing metrics.

---

## Key Methodology
- **Data Acquisition & Preprocessing:** 
  * Ingested historical Bloomberg Terminal data (`NVDA.csv`) containing paired date-value columns for NVDA, TSM, ASML, and Sentiment scores.
  * Cleaned redundant date structures, handled missing records via forward filling, and coerced timestamps to datetime objects.
- **Stationarity Transformation & Feature Engineering:**
  * Converted raw price series into daily percentage returns ($\% \Delta$) to address unit roots and non-stationarity, preventing spurious regressions.
  * Engineered 1-day lagged predictors (`TSM_Lag1`, `ASML_Lag1`) to test whether yesterday's supplier performance provides a predictive lead signal for today's NVDA return.
- **Ordinary Least Squares (OLS) Regression:**
  * Modeled current-day NVDA return ($Y$) against `TSM_Lag1`, `ASML_Lag1`, and `Sentiment` ($X$) using `statsmodels.api`.
  * Evaluated statistical significance ($p$-values, $t$-statistics) and overall goodness of fit ($R^2$, $F$-statistic).
- **Diagnostic & Econometric Validation:**
  * **Autocorrelation:** Verified residual independence using the **Durbin-Watson statistic**.
  * **Normality & Residual Distribution:** Evaluated residual properties via **Omnibus**, **Jarque-Bera (JB)**, Skewness, and Kurtosis metrics.
  * **Lead-Lag Visualization:** Generated regression plots using Seaborn (`regplot`) to visually inspect scatter trends between lagged supplier returns and current NVDA returns.

---

## Model Summary & Econometric Results

```text
                            OLS Regression Results                            
==============================================================================
Dep. Variable:                   NVDA   R-squared:                       0.007
Model:                            OLS   Adj. R-squared:                  0.001
Method:                 Least Squares   F-statistic:                     1.285
No. Observations:                 582   Prob (F-statistic):              0.279
==============================================================================
                 coef    std err          t      P>|t|      [0.025      0.975]
------------------------------------------------------------------------------
const          0.0024      0.001      1.827      0.068      -0.000       0.005
TSM_Lag1       0.0566      0.070      0.805      0.421      -0.081       0.195
ASML_Lag1     -0.0661      0.067     -0.993      0.321      -0.197       0.065
Sentiment      0.0119      0.007      1.612      0.107      -0.003       0.026
==============================================================================
Omnibus:                       78.014   Durbin-Watson:                   2.275

---

##  Technologies Used

* **Python**: Primary programming language used for data manipulation, empirical modeling, and pipeline automation.
* **Pandas & NumPy**: Core tabular and numerical operations used for time-series alignment, handling missing values, indexing, and vectorizing percentage return conversions.
* **Statsmodels**: Main econometric modeling library used for estimating Ordinary Least Squares (OLS) regressions and running statistical diagnostics (Durbin-Watson, Jarque-Bera, Omnibus tests).
* **Matplotlib & Seaborn**: Data visualization tools used to plot time-series trends and construct scatter regression plots (`regplot`) to analyze lead-lag dynamics.

---

##  Key Insights

* **Weak-Form Efficient Market Hypothesis (EMH)**: 1-day lagged supplier returns ($\text{TSM}_{\text{Lag1}}\: p=0.421$, $\text{ASML}_{\text{Lag1}}\: p=0.321$) are statistically insignificant. Information regarding supply chain partners is absorbed by the market in real time without multi-day lag opportunities.
* **Qualitative Sentiment Signal**: News sentiment was the strongest predictor ($p=0.107$, $\beta=0.0119$). While narrowly outside the 5% significance threshold ($\alpha = 0.05$), its positive correlation suggests investor psychology and narrative momentum carry over into short-term price action more persistently than hardware metrics.
* **Model Fit & Autocorrelation**: The $R^2$ of 0.007 (0.7% variance explained) is expected for high-frequency daily return noise. A Durbin-Watson statistic of 2.275 confirms minimal first-order residual autocorrelation.
Prob(Omnibus):                  0.000   Jarque-Bera (JB):              621.654
==============================================================================
