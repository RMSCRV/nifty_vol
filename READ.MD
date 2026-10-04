# NIFTY Options Volatility Research

Five notebooks that study the implied volatility of **NIFTY 50 options** using free data from NSE India. They cover the volatility smile and skew, term structure, Greeks-based risk, straddle/strangle strategies, and implied volatility against model-based forecasts.

## Project description

| Notebook | Question it answers | Main methods |
|---|---|---|
| `Volitility smile.ipynb` | How does IV vary across strikes for the nearest expiry? Is there put-call skew? | Black-Scholes IV by root-finding (`brentq`), smile plots, skew at 95% / ATM / 105% moneyness |
| `Volitility term structure.ipynb` | How does ATM IV change with time to expiry? | ATM IV for the next 8 expiries, call and put curves, slope in IV points per day |
| `Volatility risk.ipynb` | How exposed is the surface to volatility moves? | Delta, vega, vanna and volga profiles across strikes, IV shock P&L (second-order Taylor approximation) |
| `Strangle_straddle.ipynb` | Does the implied move over- or under-predict the realized move, and does selling or buying it pay? | ATM straddle and 2% OTM strangle from daily Bhavcopy files, implied vs realized move, backtest with Sharpe, drawdown and win rate, DTE breakdown |
| `IV_vs_egacrh.ipynb` | Is a single option's IV a better forecast of future volatility than a statistical model? | One historical contract's IV against rolling EGARCH(1,1) and future 21-day realized volatility, RMSE, MAE and correlation |

## Data sources

- **NSE option-chain API** (`option-chain-v3`, `option-chain-contract-info`, `allIndices`) for live chains, expiries and spot
- **NSE Bhavcopy archives** (daily F&O zip files) for historical option prices
- **Yahoo Finance** (`^NSEI`) for historical spot prices and returns in the EGARCH notebook

## Requirements

Python 3, run in Jupyter. Each notebook installs its own dependencies with `!pip`. Across the five, the packages are `requests` or `curl_cffi`, `pandas`, `numpy`, `scipy`, `matplotlib`, `yfinance`, `arch` and `scikit-learn`.

## Known limitations
- **Live notebooks are snapshots.** Smile, term structure and risk reflect the moment you run them, so results change daily.
- **Assumptions differ between notebooks.** Risk-free rates are hard-coded and inconsistent across notebooks. IV is taken from NSE in some notebooks and recomputed in others.
- **The EGARCH notebook** analyses one contract with a short sample, so its statistics are not conclusive.
- **Backtests** ignore transaction costs, slippage, margin and the bid-ask spread.