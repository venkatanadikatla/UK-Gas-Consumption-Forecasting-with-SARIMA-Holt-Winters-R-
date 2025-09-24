# UK-Gas-Consumption-Forecasting-with-SARIMA-Holt-Winters-R-
Quarterly UK natural gas consumption (1960–1986) modeled with log transform + seasonal differencing, SARIMA identification via auto.arima, full residual diagnostics (ACF/PACF, Ljung–Box), 16-quarter forecasts with back-transformation to original units, and a parallel Holt-Winters (additive) exponential smoothing fit with manual forecast checks.
# UK Gas Consumption Forecasting with SARIMA & Holt-Winters (R)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/venkatanadikatla/UKGas-SARIMA-Forecasting/blob/main/notebooks/01_ukgas_sarima_hw.ipynb)

> Time-series analysis of **UKgas** (quarterly UK natural-gas consumption, 1960–1986).  
> Workflow: log transform → seasonal differencing → ADF tests → ACF/PACF → SARIMA & Holt-Winters → diagnostics → 16-quarter forecasts → back-transform to original scale.

---

## 🔎 Summary (TL;DR)
- **Data:** `UKgas` from base R datasets (quarterly, 1960–1986, 108 obs).
- **Preprocessing:** log transform; seasonal differencing (lag=4).
- **Stationarity:** ADF confirms stationarity after seasonal differencing (ct & c models).
- **Models:**  
  - SARIMA **ARIMA(2,0,3)(1,1,0)[4]** on log data.  
  - Holt-Winters additive (level, trend, seasonality) on log data.
- **Diagnostics:** Residuals ~ white noise; Ljung–Box p ≈ 0.19 (SARIMA), p ≈ 0.21 (HW).
- **Forecasts:** 16 quarters ahead with 80/95% CIs; forecasts back-transformed (exp) to original units (millions of therms).
- **Extras:** Manual HW forecast checks reproduce `forecast()` outputs exactly.

---

## 🧠 Problem & Approach
**Goal:** Build interpretable seasonal forecasting models that (1) respect stationarity, (2) pass residual diagnostics, and (3) produce calibrated quarterly forecasts.

**Steps**
1. Explore raw series (trend + strong seasonality).  
2. **Transform:** `log(UKgas)`; **Seasonal difference:** `diff(., lag=4)`.  
3. **Stationarity tests:** ADF (`ct`, `c`, `nc`).  
4. **Identify orders:** ACF/PACF + `auto.arima()` (no drift/mean).  
5. **Fit:** SARIMA on log data; Holt-Winters on log data.  
6. **Validate:** Residual ACF/PACF, Q-Q, Ljung–Box.  
7. **Forecast:** 16Q ahead; back-transform to original units.

---

## 📈 Key Results (selected)
- **SARIMA:** ARIMA(2,0,3)(1,1,0)[4] on log data; strong diagnostics (ACF residuals within bounds; Ljung–Box p≈0.19).  
- **Holt-Winters:** α≈0.029, β≈1.0, γ≈0.725; seasonal indices consistent with winter peak (Q1), summer trough (Q3).  
- **Back-transformed forecasts:** e.g., 1987 Q1 ≈ 1,244–1,263M therms depending on model; credible seasonal pattern sustained.

---
