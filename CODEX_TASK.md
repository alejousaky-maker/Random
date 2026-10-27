# Codex Task — Personal Finance Command Center

Build a polished, professional, responsive and interactive personal finance dashboard using React + TypeScript + Vite + Recharts. The app is for a young investor and should feel like a premium wealth-management terminal, not a generic budgeting app.

## Primary objective
Create a single dashboard that helps the user make better decisions about cash, investing, portfolio risk, spending, and market timing without pretending to predict the market. The app should clearly separate facts, signals, and suggested actions.

## Current financial snapshot (seed data, Oct 27 2026)
- Net worth: $6,914.77
- 30-day net worth change: +$254.18 (+3.82%)
- Cash: $5,992.12
- Fidelity taxable brokerage: $386.85
- Fidelity Roth IRA: $535.80
- Approx asset allocation: Cash 87.5%, ETFs 8.86%, Stocks 2.33%, Mutual funds 1.31%
- Active recurring expense detected: Shopify, monthly, latest amount $1.06, historical average $9.12
- Current connected-spend data is sparse/incomplete for normal living expenses, so the UI must show a data-quality warning instead of implying spending is fully captured.

## Holdings seed
Use src/data/portfolio.json. Holdings are spread across taxable and Roth IRA accounts. Aggregate duplicate tickers across accounts while preserving account breakdown.

## Core UX
Dark premium UI by default with optional light mode. Desktop-first but fully responsive. Left nav + top market status bar. Use cards, charts, tables, signal chips, progress bars, tooltips, expandable analysis panels, and interactive sliders.

## Required pages / panels

### 1. Executive Overview
Show:
- Net worth
- Cash
- Invested assets
- Invested % of net worth
- 30-day net-worth change
- Estimated cash deployment capacity
- Current market regime
- Portfolio risk score
- Data freshness / completeness indicator

Include net-worth area chart with 1W / 1M / MAX toggle using seed history.

### 2. Portfolio
- Holdings table with ticker, account, value, cost basis, unrealized P/L, weight, daily move, asset class.
- Aggregate duplicate tickers.
- Allocation donut / bars.
- Account allocation: taxable vs Roth IRA.
- Concentration analysis.
- Asset class analysis.
- Geographic/style exposure approximations based on ticker metadata.
- Risk warnings for speculative positions, thematic overlap, gold exposure, energy exposure, international exposure, small-cap exposure.

### 3. Cash Deployment Engine
This is the most important feature.

Build a transparent score called `Deployment Score` from 0–100. It must NOT claim to identify the perfect market bottom. It should estimate how attractive it is to deploy incremental cash based on several signals.

Inputs / sub-scores:
1. Cash excess score — how much cash sits above the user-defined reserve.
2. Market drawdown score — S&P 500 decline from 52-week high.
3. Valuation score — forward P/E vs long-term average.
4. Yield competition score — 10-year Treasury yield / real yields.
5. Fed/inflation score — policy stance and inflation trend.
6. Portfolio imbalance score — whether the proposed purchase improves diversification.
7. Volatility score — optional VIX or proxy.

Default score weights:
- Cash excess 25%
- Drawdown 20%
- Valuation 15%
- Yield competition 15%
- Fed/inflation 10%
- Portfolio imbalance 10%
- Volatility 5%

Display score with explanation of every component and let user adjust weights.

Suggested action bands:
- 0–29: Hold / preserve optionality
- 30–49: Small recurring contribution only
- 50–69: Normal DCA / moderate deployment
- 70–84: Accelerated deployment
- 85–100: High-opportunity zone, still staged rather than all-in

Add a staged deployment planner. User enters deployable cash and chooses 3, 6, or 12 tranches. Show exact tranche amounts and suggested triggers (date-based + drawdown-based).

### 4. Scenario Simulator
Interactive sliders for:
- Monthly contribution
- Cash reserve target
- Expected annual return
- Inflation
- Time horizon
- Initial deployable cash

Show projected net worth over time under conservative/base/aggressive assumptions. Clearly label these as scenarios, not forecasts.

### 5. Market & Macro
Cards for:
- S&P 500 price / daily move
- S&P 500 forward P/E
- 10Y Treasury yield
- 10Y real yield
- Fed funds rate
- Inflation trend
- VIX
- Gold
- Oil

Add Market Regime classification: Risk-On, Neutral, Risk-Off, Tightening, Disinflationary Growth, Inflation Shock, etc. Include plain-English interpretation.

Seed current macro context:
- 10-year Treasury around 5.0% in late Oct 2026.
- Fed funds effective around 3.88%.
- Fed meeting Oct 27–28, 2026; market broadly expects a hold, with inflation still above target and risk of future tightening.
- S&P 500 valuation is not extremely cheap; recent forward P/E estimates are roughly high-teens.

### 6. News Intelligence
Create a news panel categorized by:
- Portfolio holdings
- Federal Reserve / rates
- Inflation
- Markets
- Energy
- Gold

Each item should have headline, source, timestamp, affected tickers, sentiment, likely impact, confidence. Add filters by ticker and relevance.

Architect news as provider adapters. Use a mock provider by default and optional live providers through environment variables. Never hardcode secret keys.

### 7. Money Health
- Cash reserve status
- Recurring expenses
- Spending trend if data is available
- Savings rate when reliable income data exists
- Emergency fund months (user-adjustable monthly expense estimate)
- Roth IRA contribution tracker (manual input)
- Taxable vs tax-advantaged contribution suggestion logic

If data is incomplete, show explicit "Insufficient connected spending data" states.

## Decision Rules
Create an `Action Center` that surfaces at most 5 high-priority actions. Examples:
- Cash allocation is unusually high; consider a staged deployment plan after setting reserve.
- Portfolio has many very small positions; consolidation may improve clarity.
- Prioritize broad-market/core exposure before adding more thematic positions.
- Roth IRA has available cash; highlight tax-advantaged contribution opportunity when appropriate.
- High Treasury yields increase the opportunity cost of equities; compare expected equity return vs risk-free alternatives.

Every action must show: reason, urgency, expected benefit, tradeoff, confidence, and whether it is based on user data or market data.

## Architecture
- React + TypeScript + Vite
- Recharts for charts
- Zustand or simple context for UI state
- No backend required for MVP
- Provider interfaces for live market/news data
- LocalStorage for user preferences and manually entered goals
- Strong TypeScript typing
- Split components logically
- Accessibility: keyboard navigation, semantic labels, adequate contrast

## Files to create
- src/App.tsx
- src/main.tsx
- src/styles.css
- src/types.ts
- src/data/portfolio.json
- src/data/networth.json
- src/data/macro.json
- src/lib/deploymentScore.ts
- src/lib/analytics.ts
- src/components/*
- README.md
- .env.example

## Quality bar
The UI should look like a professional wealth-management product. Avoid toy charts, giant gradients, neon crypto aesthetics, or unnecessary animations. Use restrained motion, clear typography, strong information hierarchy, and dense but readable analytics.

Add tooltips that explain financial metrics in simple language.

Add a prominent disclaimer: educational decision-support only, not individualized investment, tax, or legal advice.

## Final acceptance criteria
- `npm install` and `npm run dev` work.
- No TypeScript errors.
- Interactive charts and sliders work.
- Deployment Score updates live.
- Portfolio aggregation works across accounts.
- Data-quality warnings appear when data is incomplete.
- Responsive at desktop/tablet/mobile sizes.
- README explains how to replace seed data with live APIs.
