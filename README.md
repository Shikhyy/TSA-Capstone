# 📈 TSA Capstone 2026 — Data-Driven Stock Analysis on StockGro

> **Consulting & Analytics Club, IIT Guwahati**  
> Time Series Analysis Capstone Project · May 2026  
> **Author: Shikhar Verma**

---

## 🧭 Project Overview

This project applies quantitative time series forecasting to NSE-listed stocks, uses those models to construct a data-driven portfolio, and executes it on **StockGro** — a live virtual stock market simulator. The full pipeline runs from raw historical data all the way to real trades placed in the market, with every prediction compared against what actually happened.

The core question the project answers: *can time series models built on historical NSE data generate actionable portfolio decisions, and how accurately do those predictions hold up against real market outcomes?*

---

## 🗂️ Repository Structure

```
tsa-capstone-2026/
│
├── TSA_Capstone_Notebook.ipynb     # Complete pipeline — Tasks 1–8
│
├── TSA_Capstone_Report.docx         # Final report (max 10 pages)
│
├── TSA_Dashboard.html                    # Interactive dashboard (open in browser)
│
├── data/
│   ├── Forecasting_Models_Evaluation.csv
│   ├── Portfolio_Allocation_Strategy.csv
│   ├── StockGro_Execution_Summary.csv
│   └── Predicted_vs_Actual.csv
│
└── README.md
```

---

## 🎯 Problem Statement

**Data-Driven Stock Analysis using Time Series Models on StockGro**

Build predictive models on historical NSE stock data (Jan 2021–Dec 2025), use those models to allocate a virtual ₹10,00,000 portfolio on StockGro, execute the trades during a live 2-day trading window, and then compare every prediction against the actual market outcome.

---

## 🏗️ Pipeline — 8 Tasks

```
Stock Selection  →  Preprocessing  →  Forecasting  →  Volatility & Trend
      ↓                                                        ↓
  Portfolio Construction  →  Model Comparison  →  StockGro Execution  →  Performance Tracking
```

| Task | Description | Key Output |
|------|-------------|------------|
| **Task 1** | Stock universe selection across 6 NSE sectors | Justified 7-stock universe |
| **Task 2** | ADF stationarity testing, forward fill, MinMaxScaler, log returns | Clean train/test datasets |
| **Task 3** | ARIMA + Prophet + Ensemble forecasting with 80% CIs | 2-day price forecasts per stock |
| **Task 4** | GARCH(1,1) volatility + STL trend decomposition | Risk profiles and trend assessments |
| **Task 5** | Portfolio construction — Strategy A + B combined | ₹9,98,629 deployed across 7 stocks |
| **Task 6** | MAPE, RMSE, directional accuracy comparison | ARIMA selected as primary model |
| **Task 7** | Live virtual trading on StockGro (14 May 2026) | All 7 orders executed |
| **Task 8** | Predicted vs actual comparison + reflection | Live MAPE: 1.04% · Dir Acc: 43% |

---

## 📊 Models Used

| Model | Role | Avg Test MAPE |
|-------|------|--------------|
| **ARIMA** (auto_arima / AIC) | Primary forecasting model | **1.04%** |
| **Facebook Prophet** | Trend + seasonality with 80% CI | 16.28% |
| **Ensemble** (60% ARIMA + 40% Prophet) | Secondary directional signal | 7.29% |
| **GARCH(1,1)** | Time-varying volatility → portfolio weights | D+1 vol forecast per stock |
| **STL Decomposition** | Trend direction and strength | Trend strength > 0.90 for all stocks |

---

## 💼 Stock Universe

| Stock | Sector | Ann. Vol | Trend | Trend Strength |
|-------|--------|----------|-------|---------------|
| RELIANCE | Energy / FMCG | 22.0% | ⬆ Upward | 0.99 |
| HDFCBANK | Banking | 18.8% | ⬆ Upward | 0.96 |
| TCS | IT | 20.8% | ⬆ Upward | 0.93 |
| SUNPHARMA | Pharma | 23.7% | ⬆ Upward | 0.97 |
| MARUTI | Auto | 25.7% | ⬇ Downward | 0.97 |
| NESTLEIND | FMCG | 16.6% | ⬆ Upward | 0.90 |
| ICICIBANK | Banking | ~20% | ⬆ Upward | Live addition |

Stocks were selected using 30-day rolling annualised volatility, STL trend analysis, and sector-based rationale to ensure diversification across uncorrelated industries.

---

## 📐 Portfolio Allocation Strategy

Two quantitative strategies were combined:

**Strategy A — Forecast-Guided (40% weight)**  
Stocks ranked by ARIMA predicted 5-day return. Capital allocated proportionally to positive signals.

**Strategy B — Volatility-Aware (60% weight)**  
Inverse GARCH D+1 volatility weights: `wᵢ = (1/σ̂ᵢ) / Σⱼ(1/σ̂ⱼ)`  
Lower volatility → higher allocation.

**Combined:** `w_final = 0.60 × w_B + 0.40 × w_A`

| Stock | Weight | Deployed | Entry Price |
|-------|--------|----------|-------------|
| SUNPHARMA | 29.4% | ₹2,94,030 | ₹1,837.69 |
| NESTLEIND | 24.5% | ₹2,44,776 | ₹1,431.44 |
| RELIANCE | 16.7% | ₹1,66,670 | ₹1,344.11 |
| HDFCBANK | 10.4% | ₹1,04,281 | ₹766.77 |
| MARUTI | 10.4% | ₹1,03,390 | ₹12,923.80 |
| TCS | 6.2% | ₹61,907 | ₹2,210.96 |
| ICICIBANK | 2.4% | ₹23,575 | ₹1,240.81 |
| **Total** | **100%** | **₹9,98,629** | |

---

## 🏦 StockGro Execution

- **Platform:** StockGro — Portfolio: Time Series Analysis 2026
- **Day 1 (BUY):** 14 May 2026 · All 7 orders placed between 14:05–14:37 IST
- **Day 2 (SELL):** 15 May 2026 · Auto-close at 15:25 IST
- **Deployment rate:** 99.86% (₹1,370 cash remaining — below minimum lot size)

---

## 🎯 Final Results — Predicted vs Actual

| Stock | Buy ₹ | ARIMA Pred | Actual Close | MAPE | Direction | P&L | Result |
|-------|--------|-----------|-------------|------|-----------|-----|--------|
| SUNPHARMA | 1,837.69 | 1,839.12 | 1,848.08 | 0.48% | ✅ Hit | +₹1,662 | **Winner** |
| TCS | 2,210.96 | 2,213.00 | 2,220.01 | 0.32% | ✅ Hit | +₹253 | **Winner** |
| MARUTI | 12,923.80 | 12,930.00 | 12,994.57 | 0.50% | ✅ Hit | +₹566 | **Winner** |
| RELIANCE | 1,344.11 | 1,345.00 | 1,322.53 | 1.70% | ❌ Miss | −₹2,676 | Loser |
| NESTLEIND | 1,431.44 | 1,432.00 | 1,416.79 | 1.07% | ❌ Miss | −₹2,505 | Loser |
| HDFCBANK | 766.77 | 767.50 | 754.99 | 1.66% | ❌ Miss | −₹1,602 | Loser |
| ICICIBANK | 1,240.81 | 1,242.50 | 1,223.12 | 1.58% | ❌ Miss | −₹336 | Loser |
| **Portfolio** | | | | **1.04% avg** | **3/7 = 43%** | **−₹4,638** | **−0.464%** |

> **StockGro verified:** Overall Returns = −₹4,637.69 (−0.47%) ✓

---

## 📉 Key Findings

**What the models got right:**
- ARIMA achieved a live MAPE of **1.04%** in real NSE market conditions — the model correctly estimated prices to within ₹1 per ₹100 invested. This is the headline result.
- GARCH-based volatility sizing correctly limited MARUTI (highest vol at 1.62%), which turned out to be a winner.
- SUNPHARMA was the standout: correct direction, lowest MAPE (0.48%), highest return (+₹1,662).

**What the models got wrong:**
- Directional accuracy was **43% (3/7)** — near-random, consistent with the Efficient Market Hypothesis at 2-day horizons.
- RELIANCE and HDFCBANK fell due to broad energy and banking sector weakness on 15 May — a macro event a univariate model has no mechanism to anticipate.
- Prophet catastrophically overfit TCS (MAPE 51.2%) due to trend extrapolation on a volatile series.

**Core learning:**  
Time series models are excellent at estimating *how much* prices will move (1.04% MAPE), but near-random at predicting *which direction* at short horizons. The GARCH-based portfolio sizing was the most validated component of the pipeline — it adds value in risk management, not direction prediction.

---

## 🖥️ Interactive Dashboard

The project includes a fully self-contained **interactive HTML dashboard** (`TSA_Dashboard.html`) with 7 tabs:

| Tab | Content |
|-----|---------|
| 📊 Overview | Live P&L per stock, capital allocation donut, holdings table |
| 📈 Forecasts | Per-stock ARIMA forecast vs actual with live MAPE and direction result |
| 💼 Portfolio | Deployment bar, sector pie, correlation heatmap, Strategy A vs B vs Combined |
| ⚡ Volatility | GARCH(1,1) conditional vol per stock with 30-day rolling comparison |
| 📉 Trend & STL | STL decomposition — price vs trend, trend strength bar chart |
| 🔬 Model Comparison | MAPE/RMSE/DirAcc comparison table and charts across all 3 models |
| 🎯 Final Results | Predicted vs actual price comparison, return % per stock, full verified table |

> Open `TSA_Dashboard.html` in any browser — no installation, no server needed.

---

## ⚙️ How to Run the Notebook

```bash
# Install dependencies
pip install yfinance pandas numpy matplotlib seaborn statsmodels \
            scikit-learn prophet pmdarima arch scipy

# Open notebook
jupyter notebook TSA_Capstone_Notebook_FINAL.ipynb
```

The notebook fetches real data via `yfinance` automatically. If yfinance is unavailable (e.g. offline environment), it falls back to a synthetic GBM simulation using realistic NSE price ranges and volatility profiles. All StockGro trade prices are hardcoded in Tasks 7 and 8.

**Python version:** 3.9+  
**Key libraries:** `pmdarima`, `prophet`, `arch`, `statsmodels`, `scikit-learn`

---

## 📋 Deliverables

| File | Description |
|------|-------------|
| `TSA_Capstone_Notebook.ipynb` | Full pipeline notebook — Tasks 1–8 |
| `TSA_Capstone_Report.docx` | Final report — max 10 pages, all sections |
| `TSA_Dashboard.html` | Interactive dashboard — open in browser |
| `Forecasting_Models_Evaluation.csv` | ARIMA / Prophet / Ensemble metrics + live results |
| `Portfolio_Allocation_Strategy.csv` | Full allocation table with strategy rationale |
| `StockGro_Execution_Summary.csv` | All 14 trades (7 buys + 7 sells) with timestamps |
| `Predicted_vs_Actual.csv` | Forecast vs actual comparison, MAPE, P&L per stock |

---

## 👤 Author

**Shikhar Verma**  
Consulting & Analytics Club, IIT Guwahati  
TSA Capstone 2026 · Submission: 17 May 2026

---

## 📄 License

This project was submitted as part of the TSA Capstone 2026 organised by the Consulting & Analytics Club, IIT Guwahati in collaboration with StockGro. All trade data is from the StockGro virtual platform — no real money was involved.
