<h1 align="center">Taiwan Stock Forecasting Research</h1>

##   Overview

This repository collects two related research projects on **forecasting the Taiwan stock market** using machine learning. Both studies use TWSE historical data and benchmark against the Taiwan Weighted Stock Index (TWII).

| # | Project | Method | Key Result | Paper |
|---|---------|--------|------------|-------|
| 1 | **NSTC Undergraduate Research** *(Jul 2025 – Feb 2026)* | Multi-level momentum & liquidity-volatility factors + (XGBoost / LightGBM / RF / GBRT / NN) | Nonlinear models beat linear regression by **~50%** on backtest returns | [運用機器學習分析多層次動能與流動性波動度之研究](papers/國科會大專生研究計畫成果報告.pdf) |
| 2 | **Hybrid Hierarchical Deep Learning (HHDL)** *(Sept 2025 – Jan 2026)* | HFSLS feature selection + PSO-tuned BIGRU | **R² = 0.937** on TWII; HFSLS contributes 97% of the gain | [分層股票預測模型](papers/Hybrid%20Hierarchical%20Deep%20Learning%20Framework%20for%20Stock%20Forecasting%20in%20the%20Taiwan%20Stock%20Market.pdf) |

---

##  Project 1 — An Empirical study on multi-level momentum and votality liquidity Using machine learning
### Data
- Taiwan stock market historical data, **Jan 1999 – Feb 2025**

### Factors
A multi-level factor set capturing both momentum and volatility signals:
- Short-term momentum
- Long-term momentum
- Momentum change
- Maximum single-period return
- Return volatility

### Models
Linear baseline vs. nonlinear ensembles:
- Linear regression *(baseline)*
- **XGBoost**
- **LightGBM**
- **Random Forest**
- **GBRT**
- **NN**

### Findings
- Nonlinear ensemble models **consistently outperformed** linear regression on both predictive accuracy and backtest returns.
- Tree-based methods captured **nonlinear interactions** between momentum factors and extreme returns.
- Equal-partition ranking enabled flexible portfolio construction for diversified allocation and risk management.
- Backtest portfolios delivered superior cumulative returns vs. the **TWII** benchmark.
  
---

##  Project 2 — Hybrid Hierarchical Deep Learning Framework for Stock Forecasting in the Taiwan Stock Market

### Key Results
- **R² = 0.937** on the Taiwan Weighted Stock Index (TWII).
- **HFSLS feature selection alone contributes 97%** of the total performance gain — the most critical component.
- Cross-industry validation:
  - Defensive sectors: predicted accurately
  - Tech sectors: predicted accurately
  - Cyclical sectors: more volatile (as expected), but turning points still captured

### Practical Value
- Captures **key market turning points** missed by classical models.
- Provides a **quantitative investment tool** suitable for portfolio decisions.
