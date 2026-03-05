# Revenue Accrual and Fee Reconciliation Engine

**Sara Iqbal** | MSc Data Science | Portfolio Project

[Live Dashboard](https://sara-iqbal.github.io/Revenue-Accrual-Fee-Reconciliation-Engine/) | [Google Colab Notebook](https://sara-iqbal.github.io/Revenue-Accrual-Fee-Reconciliation-Engine/) | [LinkedIn](https://www.linkedin.com/in/saraiqbaldata0602/)

---

## What This Project Is

This project automates the monthly revenue accounting cycle for a simulated fund management business. It covers everything from generating daily AUM data, calculating management fees using tiered fee schedules, posting journal entries, producing P&L statements by fund, and reconciling the calculated fees against what an external administrator reported.

The project is built to reflect how a Global Revenue Accounting team at a firm like BlackRock actually operates — preparing monthly accruals, identifying variances, classifying breaks by root cause, and producing audit-ready schedules.

---

## Why I Built This

The Global Revenue Accounting Analyst role requires someone who can handle large volumes of financial data accurately, implement process improvements, prepare balance sheet reconciliations, and liaise with external administrators to resolve variances in AUM and advisory fees. Rather than describing those skills in a cover letter, I built a working system that does them.

---

## What the Project Does

The pipeline runs in twelve steps:

1. Defines a fund universe of 10 funds across four types — Equity, Fixed Income, Multi-Asset, and Money Market — with three share classes each: Institutional, Retail, and Clean
2. Applies tiered management fee schedules to each fund type, calibrated to real institutional asset management practice
3. Generates 365 days of daily AUM data for each fund using geometric Brownian motion with realistic volatility and net fund flows
4. Calculates daily fee accruals by applying the blended tiered rate to each day's AUM and dividing by 365
5. Aggregates daily accruals into monthly revenue figures per fund per share class
6. Applies fee waivers where triggered, producing net revenue after waiver
7. Posts journal entries for each monthly period — management fee receivable debit, revenue credit, and waiver expense where applicable
8. Produces an annual P&L statement by fund showing gross revenue, waivers, net revenue, operating costs, operating profit, and margin
9. Simulates what an external administrator would have calculated, introducing realistic discrepancies such as timing differences, rounding, fee rate mismatches, and waivers not applied
10. Reconciles the two figures, flags any variance above 0.01% of AUM as a break, classifies the root cause, and assigns a resolution status
11. Tracks the monthly break rate trend and total variance amounts
12. Exports a six-sheet Excel audit schedule and saves all data to CSV and JSON

---

## Tools Used

Python, Pandas, NumPy, openpyxl, Plotly, Chart.js

---

## Fund Universe

| Fund | Type | Base AUM |
|---|---|---|
| BlackRock Core Equity Fund | Equity | $4.2B |
| BlackRock Emerging Markets Fund | Equity | $1.85B |
| BlackRock Aggregate Bond Fund | Fixed Income | $6.8B |
| BlackRock High Yield Bond Fund | Fixed Income | $2.3B |
| BlackRock Government Bond Fund | Fixed Income | $5.1B |
| BlackRock Balanced Growth Fund | Multi-Asset | $3.4B |
| BlackRock Conservative Alloc Fund | Multi-Asset | $1.6B |
| BlackRock USD Money Market Fund | Money Market | $9.2B |
| BlackRock EUR Money Market Fund | Money Market | $4.7B |
| BlackRock ESG Equity Fund | Equity | $2.9B |

---

## Fee Schedule

Tiered management fees applied by fund type, with share class discounts on top.

| Fund Type | First $500M | Next $500M | Next $4B | Above $5B |
|---|---|---|---|---|
| Equity | 75 bps | 65 bps | 55 bps | 45 bps |
| Fixed Income | 40 bps | 35 bps | 30 bps | 25 bps |
| Multi-Asset | 60 bps | 55 bps | 50 bps | 45 bps |
| Money Market | 15 bps | 12 bps | — | 10 bps |

Share class discounts: Retail minus 15%, Clean minus 25%, Institutional no discount.

---

## Results

| Metric | Value |
|---|---|
| Total AUM modelled | $42.1B |
| Monthly fee calculations automated | 1,080 (10 funds x 3 classes x 12 months) |
| Annual gross accrual | $198.2M |
| Fee waivers applied | $10.8M |
| Annual net revenue | $187.4M |
| Operating profit | $157.7M |
| Operating margin | 84.2% |
| Total reconciliation series | 1,080 |
| Breaks flagged (variance above 0.01%) | 32 (3.0%) |
| Pre-investigation accuracy | 99.7% |
| Post-resolution accuracy | 100.0% |
| Escalated breaks | 3 (0.28%) |
| Journal entries posted | 3,240+ |

---

## Reconciliation Break Root Causes

| Cause | Count |
|---|---|
| Data timing difference | 11 |
| AUM rounding difference | 9 |
| Fee rate mismatch | 8 |
| Waiver not applied | 4 |

All 29 resolved breaks were identified, classified, and closed. 3 were escalated for further investigation.

---

## Audit Schedule Export

The notebook exports a six-sheet Excel file covering:

- Revenue Summary — annual P&L per fund with gross revenue, waivers, net revenue, operating costs, and margin
- Monthly Accruals — 1,080 rows of monthly accrual data per fund per share class
- Reconciliation Detail — full BLK vs administrator comparison for all 1,080 series
- Breaks and Exceptions — filtered view of all 32 breaks with root cause and resolution status
- Journal Entries — complete ledger of all debit, credit, and waiver entries posted
- P&L Variance Analysis — annual variance between BLK totals and administrator totals by fund in dollars and basis points

---

## How to Run

Open the notebook in Google Colab. Run all cells from top to bottom. No API keys or external data sources required — all data is generated within the notebook. The Excel audit schedule and JSON dashboard data are saved automatically at the end.

---

## Dashboard

The GitHub Pages dashboard has five tabs: Overview, Fee Accruals, P&L Statements, Reconciliation, and Audit Schedules. The reconciliation tab lets you filter by fund, period, and break status and run the reconciliation live to see the results update.

---

## Conclusion

This project covers the core technical tasks of a revenue accounting analyst role — monthly accruals, fee calculations, variance reconciliation, root cause analysis, and audit schedule preparation — and automates them end to end. The reconciliation engine flagged 32 breaks across 1,080 series, classified every one by root cause, and produced a clean audit trail with zero unresolved items after investigation. The approach replaces an estimated four hours of manual Excel work per fund per month with a single notebook run.

---

## Repository Structure

```
revenue-accrual-reconciliation-engine/
    index.html                    — live GitHub Pages dashboard
    revenue_accrual_engine.ipynb  — full Google Colab notebook
    README.md                     — this file
```

---

## Other Projects

| Project | Tools | Description |
|---|---|---|
| Bond Index Replication and Rebalancing Engine | Python, SciPy, NumPy, Pandas | 150-bond replication of iShares LQD benchmark, tracking error 8.4 bps, IR 0.87 |
| Nexus Wealth Capital and Balance Sheet Optimizer | Python, Pandas, Streamlit | Basel III RWA engine, LCR monitoring, Economic Profit Waterfall |
| Real-Time Credit Card Fraud Detection | Python, XGBoost, SHAP, Gradio | ROC-AUC 97.4%, F1 82.1% on 284,807 transactions |
| Algorithmic Trading Signal Engine | Python, PyTorch, LSTM, Streamlit | Directional accuracy 67.3%, Sharpe 1.42 |
| Financial News Sentiment Analyser | Python, FinBERT, Hugging Face | Test accuracy 87.3%, F1 Macro 0.861 |
