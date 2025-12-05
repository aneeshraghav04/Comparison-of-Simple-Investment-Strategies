# Value vs Momentum Strategies on Indian Large-Cap Stocks (NSE)

This project implements and compares two systematic equity strategies — **Value** and **Momentum** — on large-cap Indian stocks listed on the National Stock Exchange (NSE). The analysis uses publicly available index constituents (Nifty 50) and market data sourced through Yahoo Finance.

The strategies are constructed using a common universe, converted into equal-rupee portfolios, and evaluated via cross-sectional metrics and overlap of holdings.

---

## 🔍 Project Overview

### 1. Universe: Nifty 50 Constituents
- The list of NIFTY 50 companies is sourced directly from the official NSE Indices CSV.
- Tickers are mapped to Yahoo Finance by appending `.NS` (e.g., `RELIANCE` → `RELIANCE.NS`).
- All strategy data is retrieved dynamically — no local datasets required.

### 2. Data Source
All fundamentals and price history are obtained using **Yahoo Finance** via the `yfinance` Python package:
- Current price
- Market capitalization
- P/E, P/B, P/S ratios
- Enterprise Value, EBITDA, Gross Profit
- Daily adjusted closing prices

---

## 📈 Strategy 1: Value (Relative Valuation)

The Value strategy ranks stocks based on multiple valuation factors:

- Price-to-Earnings (P/E)
- Price-to-Book (P/B)
- Price-to-Sales (P/S)
- Enterprise Value / EBITDA (EV/EBITDA)
- Enterprise Value / Gross Profit (EV/GP)

Each metric is converted into a cross-sectional percentile within the universe, and a **Value Score** (average percentile) is computed.

> **Lower score = cheaper stock relative to peers**

The portfolio selects the top `N` cheapest stocks (based on the Value Score) and allocates equal rupee capital across them.

---

## 🚀 Strategy 2: Momentum (Multi-Horizon Return Strength)

The Momentum strategy captures recent relative price strength using four time horizons:

- One-year return (~252 trading days)
- Six-month return (~126 days)
- Three-month return (~63 days)
- One-month return (~21 days)

Each return is turned into a percentile ranking across the universe.  
The **Momentum Score** is the average of these percentiles.

> **Higher score = stronger and more persistent momentum**

The strategy selects the top `N` strongest momentum stocks and allocates equal capital across them.

---

## 📊 Evaluation & Comparison

The notebook compares the two resulting portfolios using:

- Number of holdings
- Average stock price
- Median market capitalization
- Average composite score (Value Score or Momentum Score)
- Estimated invested rupees
- Overlap in holdings (tickers selected by both strategies)

This helps understand whether “cheap” stocks and “strong recent performers” intersect or diverge in the Indian large-cap universe.

---

## 🧪 Methodological Notes

- Percentile-based scoring normalizes metrics and avoids unit biases.
- Stocks with missing or invalid data are excluded from scoring.
- Enterprise Value ratios (EV/EBITDA, EV/GP) are only used when financially meaningful.
- All portfolios are equal-weighted for consistency and comparability.

---

## 🛠 Requirements

Install dependencies using:

```bash
pip install pandas numpy yfinance requests
