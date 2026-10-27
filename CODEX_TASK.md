# Codex Task — Personal Finance Command Center

Build a polished, professional, responsive and interactive personal finance dashboard using React + TypeScript + Vite + Recharts.

## Goal
Create a single decision-support dashboard for net worth, cash, investments, portfolio risk, recurring spending, macro conditions, market news, and staged investment deployment. It must be useful without pretending to predict a perfect market bottom.

## Privacy requirement
DO NOT commit real balances, account numbers, holdings quantities, or other personal finance data to this repository. Use demo/sample values in version control. Load real user data only from ignored local files or environment-backed/private APIs.

Add these to `.gitignore`:
- `src/data/private/`
- `*.private.json`
- `.env.local`

## Required modules

### 1. Executive Overview
Show:
- Net worth
- Cash
- Invested assets
- Invested % of net worth
- 30-day net-worth change
- Estimated deployable cash after reserve
- Current market regime
- Portfolio risk score
- Data freshness/completeness indicator

Include a net-worth chart with 1W / 1M / MAX toggle.

### 2. Portfolio
- Holdings table with ticker, account, value, cost basis, unrealized P/L, weight, daily move, and asset class.
- Aggregate duplicate tickers while preserving account detail.
- Allocation charts.
- Taxable vs Roth/retirement allocation.
- Concentration analysis.
- Geographic/style exposure approximations using ticker metadata.
- Warnings for speculative concentration, thematic overlap, commodities, energy, international, and small-cap exposure.

### 3. Cash Deployment Engine
Create a transparent `Deployment Score` from 0–100. This estimates how attractive it is to deploy incremental cash based on conditions; it must never claim to know the perfect market bottom.

Sub-scores:
1. Cash excess score — cash above user-defined reserve.
2. Market drawdown score — S&P 500 decline from 52-week high.
3. Valuation score — forward P/E vs historical context.
4. Yield competition score — 10Y Treasury / real yields.
5. Fed/inflation score — policy stance and inflation trend.
6. Portfolio imbalance score — whether a proposed purchase improves diversification.
7. Volatility score — VIX or proxy.

Default weights:
- Cash excess 25%
- Drawdown 20%
- Valuation 15%
- Yield competition 15%
- Fed/inflation 10%
- Portfolio imbalance 10%
- Volatility 5%

Action bands:
- 0–29: Hold / preserve optionality
- 30–49: Small recurring contribution only
- 50–69: Normal DCA / moderate deployment
- 70–84: Accelerated deployment
- 85–100: High-opportunity zone, still staged rather than all-in

Let the user adjust weights and see exactly why the score changes.

Add a staged deployment planner. User enters deployable cash and selects 3, 6, or 12 tranches. Show exact tranche amounts plus date-based and drawdown-based triggers.

### 4. Scenario Simulator
Interactive sliders for:
- Monthly contribution
- Cash reserve target
- Expected annual return
- Inflation
- Time horizon
- Initial deployable cash

Show conservative/base/aggressive net-worth scenarios. Label them as scenarios, not forecasts.

### 5. Market & Macro
Cards for:
- S&P 500
- Forward P/E
- 10Y Treasury yield
- 10Y real yield
- Fed funds rate
- CPI/core inflation trend
- VIX
- Gold
- Oil

Classify the market regime, e.g. Risk-On, Neutral, Risk-Off, Tightening, Disinflationary Growth, Inflation Shock. Add a plain-English interpretation.

### 6. News Intelligence
Create a categorized news feed for:
- Portfolio holdings
- Federal Reserve / rates
- Inflation
- Markets
- Energy
- Gold

Each item: headline, source, timestamp, affected tickers, sentiment, likely impact, relevance, confidence. Filter by ticker and topic.

Use provider adapters with mock data by default and optional live providers via environment variables. Never hardcode secret keys.

### 7. Money Health
- Cash reserve status
- Recurring expenses
- Spending trend if reliable data exists
- Savings rate only when reliable income exists
- Emergency fund months from user-adjustable monthly expense estimate
- Roth/retirement contribution tracker
- Taxable vs tax-advantaged contribution decision support

If data is incomplete, explicitly show an insufficient-data state rather than a misleading zero.

### 8. Action Center
Surface at most five high-priority actions. Every action must show:
- Reason
- Urgency
- Expected benefit
- Tradeoff
- Confidence
- Whether based on user data or market data

Examples:
- Cash allocation is high relative to the selected reserve target.
- Portfolio has too many tiny positions and may benefit from simplification.
- Strengthen broad-market/core exposure before adding more thematic exposure.
- Consider tax-advantaged space before taxable additions where appropriate.
- Compare equity deployment against the current risk-free yield environment.

## Architecture
- React + TypeScript + Vite
- Recharts
- Zustand or React Context
- LocalStorage for preferences and manually entered goals
- Provider interfaces for market/news data
- Strong typing
- Accessible keyboard navigation and semantic labels
- Responsive desktop/tablet/mobile design

## Files
Create at minimum:
- `src/App.tsx`
- `src/main.tsx`
- `src/styles.css`
- `src/types.ts`
- `src/data/demoPortfolio.json`
- `src/data/demoNetWorth.json`
- `src/data/demoMacro.json`
- `src/lib/deploymentScore.ts`
- `src/lib/analytics.ts`
- `src/providers/marketProvider.ts`
- `src/providers/newsProvider.ts`
- `src/components/*`
- `.env.example`
- `.gitignore`
- `README.md`

## UX quality bar
Premium wealth-management terminal aesthetic. Dark mode by default, optional light mode. Clear typography, restrained motion, dense but readable analytics. Avoid neon crypto aesthetics, oversized gradients, or toy charts.

Add simple tooltips for financial metrics.

Include a visible disclaimer: educational decision-support only; not individualized investment, tax, or legal advice.

## Acceptance criteria
- `npm install` works.
- `npm run dev` works.
- No TypeScript errors.
- Charts and sliders are interactive.
- Deployment Score updates live.
- Duplicate holdings aggregate correctly.
- Data-quality warnings appear when data is incomplete.
- No private financial data is committed.
- README explains how to inject real data locally and how to configure live market/news providers.
