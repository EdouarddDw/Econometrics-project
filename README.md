# The Dynamics of Financial Returns

**Econometric Methods I · Maastricht University · May 2026**
Edouard Dewaerheijd, Yves Seuren, Finn Leitz

📄 **[Read the full paper (PDF)](EM_Mid_Term_Case.pdf)**

---

## Overview

This project studies the first and second moments of daily stock returns: whether returns can be predicted from their own past values, and whether volatility changes over time. We analyse daily adjusted closing prices from January 2010 to December 2024 for four large companies from different sectors, benchmarked against the S&P 500.

| Ticker | Company | Sector |
|---|---|---|
| AAPL | Apple Inc. | Technology |
| LMT | Lockheed Martin | Defense |
| JPM | JPMorgan Chase & Co. | Financials |
| SHEL | Shell plc | Energy |
| ^GSPC | S&P 500 | Market index |

All analysis uses daily log-returns, $r_t = \ln(P_t / P_{t-1})$.

## A note on the code

Almost all of the econometric work was done in **EViews**, which is point-and-click software. That is why this repository contains **no estimation code**. The results, tables and figures are all in the [paper](EM_Mid_Term_Case.pdf).

The only scripted step was data collection. We downloaded prices from Yahoo Finance with R (`tidyquant`) and filled missing trading days (holidays) with the average of the surrounding prices.

## Methods

- **Descriptive statistics:** mean, standard deviation, skewness, kurtosis and Jarque–Bera normality tests
- **Autocorrelation:** first-order residual autocorrelation and lagged-return predictability tests
- **Heteroskedasticity:** ARCH test on squared residuals
- **Robust inference:** re-estimation with heteroskedasticity-consistent standard errors (HCSE)
- **Forecasting:** static one-step-ahead return forecasts on a 500-observation hold-out, evaluated by RMSE
- **Volatility modelling:** ARCH(1) models and forecasted variances
- **Granger causality:** cross-asset lagged-return regressions with HCSE
- **CAPM:** market betas with OLS and HCSE confidence intervals

## Key findings

- **Returns are not normal.** All five series are negatively skewed with fat tails, and Jarque–Bera rejects normality in every case.
- **Returns are barely predictable.** Only JPM and the S&P 500 show a significant lagged-return effect under HCSE. It is negative, which suggests short-term reversal, but the adjusted R² stays close to zero.
- **Volatility clusters.** ARCH effects are strongly significant for every asset, and the effect is strongest for the S&P 500 (γ ≈ 0.51).
- **ARCH helps with uncertainty, not with point forecasts.** ARCH(1) slightly increases return-forecast RMSE, but it captures time-varying risk such as the 2020 volatility spike.
- **Cross-asset predictability is limited.** Lagged AAPL returns Granger-cause JPM and SHEL, but explanatory power is very small.
- **Market exposure is clear.** All betas are highly significant. JPM (1.21) and AAPL (1.11) are more sensitive than the market, while LMT (0.69) is the most defensive. HCSE widens the beta confidence intervals, which shows that plain OLS understates the uncertainty.

## Tools

EViews · R (`tidyquant`) · LaTeX
