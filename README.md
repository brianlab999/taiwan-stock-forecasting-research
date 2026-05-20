<h1 align="center">Taiwan Stock Forecasting Research</h1>

##   Overview

This repository collects two related research projects on **forecasting the Taiwan stock market** using machine learning and deep learning. Both studies use TWSE historical data and benchmark against the Taiwan Weighted Stock Index (TWII).

| # | Project | Method | Key Result | Paper |
|---|---------|--------|------------|-------|
| 1 | **NSTC Undergraduate Research** *(Jul 2025 – Feb 2026)* | Multi-level momentum & liquidity-volatility factors + (XGBoost / LightGBM / RF / GBRT / NN) | Nonlinear models beat linear regression by **~50%** on backtest returns | [An Empirical Study on Multi-Level Momentum and Volatility Using Machine Learning](papers/An Empirical Study on Multi-Level Momentum and Volatility Using Machine Learning.pdf) |
| 2 | **Hybrid Hierarchical Deep Learning (HHDL)** *(Sept 2025 – Jan 2026)* | HFSLS feature selection + PSO-tuned BiGRU | **R² = 0.937** on TWII; HFSLS contributes 97% of the gain | [Hybrid Hierarchical Deep Learning Framework for Stock Forecasting in the Taiwan Stock Market](papers/Hybrid%20Hierarchical%20Deep%20Learning%20Framework%20for%20Stock%20Forecasting%20in%20the%20Taiwan%20Stock%20Market.pdf)
---

## Project 1 — An Empirical Study on Multi-Level Momentum and Volatility Using Machine Learning

### Data
- Taiwan stock market monthly data (TEJ database), **Jan 1999 – Feb 2025** (26 years of full market-cycle coverage)
- Cross-section of **964 TWSE-listed companies** with monthly factor values
- Predicted target: next-period **Information Coefficient (IC)** of each factor; portfolios then ranked into equal partitions (10 / 20 / 50 / 100 / 192 / 964 groups) and compared against the **Taiwan Weighted Stock Index (TWII)**

### Features
A multi-level factor set capturing both momentum and volatility signals:
- **mom1m** — one-month (short-term) momentum
- **mom12m** — twelve-month (long-term) momentum
- **chmom** — six-month momentum change (acceleration)
- **maxret** — maximum single-period return (extreme-return capture)
- **retvol** — return volatility (risk dimension)

### Models
Linear baseline vs. nonlinear ML / deep models:
- **OLS** *(linear regression baseline)*
- **Random Forest**
- **GBRT** · **LightGBM** · **XGBoost** *(gradient-boosted trees)*
- **Neural Networks** (NN1–NN5, varying 1–5 hidden layers)

### Findings
- **Winning rate vs. market:** Random Forest, NN2, and NN4 each achieved a **100% monthly winning percentage** against the TWII across the full 134-month evaluation window; LightGBM, XGBoost, NN3, and NN5 all exceeded 50%, while OLS only reached 54% — confirming nonlinear models’ structural edge.
- **Risk-adjusted return:** Random Forest delivered Sharpe ratios of **0.337 / 0.427 / 0.429** on the top-10 / top-20 / top-50 partitions, and XGBoost reached **~0.30** consistently — both **far above the TWII benchmark of 0.174**, validating their ability to extract risk-efficient alpha.
- **Out-of-sample R²:** Random Forest attained the highest **R² = 0.763**, followed by NN3 (0.739), NN4 (0.621), and NN5 (0.525). OLS collapsed to **R² = −3.742**, showing that linear assumptions completely fail to capture the joint nonlinear interactions among momentum and volatility factors.
- **Cumulative return (Jan 1999 – Feb 2025, 964 partitions):** Random Forest grew capital by **+6.07×**, vs. TWII +0.99× — a roughly **6× outperformance**. Final ranking by cumulative return: **Random Forest > Neural Networks > Gradient Boosting > OLS**, with finer partitions consistently amplifying the ML advantage.
  
---

## Project 2 — Hybrid Hierarchical Deep Learning Framework for Stock Forecasting in the Taiwan Stock Market

### Data
- Taiwan stock market historical data (TEJ Pro database), **Jan 2020 – Sept 2025** (daily closing prices)
- Chronological 70/30 train-test split (train: 2020/01 – 2023/12 · test: 2024/01 – 2025/09)
- Targets: **TAIEX** (market index) + 4 representative individual stocks across industries
  - **TSMC** (semiconductor) · **Evergreen Marine** (shipping) · **MediaTek** (IC design) · **Uni-President** (retail)

### Features
A high-dimensional **Alpha158** feature set (158 technical indicators) refined by hierarchical feature selection:
- Price-volume indicators (OHLC, volume, VWAP)
- Trend indicators (MA 5/10/20/30/60, K-line patterns)
- Momentum indicators (Rate of Change, Raw Stochastic Value)
- Volatility & correlation (standard deviation, range extremes, Beta)
- **HFSLS** (Hierarchical Feature Selection with Local Shuffling) applied to reduce redundancy

### Models
Baseline vs. proposed hybrid architecture:
- **BIGRU** *(baseline — bidirectional gated recurrent unit)*
- **PSO-BIGRU** *(hyperparameter optimization only)*
- **HFSLS-BIGRU** *(feature selection only)*
- **HFSLS-PSO-BIGRU** *(proposed full model)*

### Findings
- The full **HFSLS-PSO-BIGRU** model delivered a **+2.394 absolute increase in R²** and a **97.1% reduction in MSE** vs. the baseline BIGRU on TAIEX prediction.
- Ablation analysis showed **HFSLS is the dominant driver** — contributing ~97% of total performance gain; PSO applied alone actually *hurt* performance (−1.661 R², +69.6% MSE), confirming feature selection must precede hyperparameter tuning in high-dimensional financial data.
- Cross-industry robustness: average **R² = 0.926** (std 0.029) across five targets vs. baseline’s 0.088 (std 0.656); the proposed model achieved best performance in **4 out of 5** prediction targets, generalizing well across defensive, tech, and cyclical sectors.
- Long-short backtest (Jan 2024 – Aug 2025) produced **win rates >86%** on all four stocks, with strategy returns of **598.82% (Evergreen)**, **563.71% (MediaTek)**, and **356.86% (TSMC)** — substantially exceeding both buy-and-hold and the TAIEX benchmark, with profit factor reaching **29.53** on Evergreen.
