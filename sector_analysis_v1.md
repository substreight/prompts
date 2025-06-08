# {{date}} — {{sector_name}} Sector Daily Analysis  
*Data captured at 16:30 ET from public endpoints or free web downloads.*

## Executive Summary (≤ 120 words)
| Thesis | Conviction (1–10) | Horizon | Primary Catalyst | 95 % CI Return |
|--------|------------------|---------|------------------|----------------|
| {{thesis_sentence}} | {{conviction}} | {{horizon}} | {{catalyst}} | {{ci_range}} |

*Key risk-adjusted alpha stems from {{strategy_stub}} exploiting a {{sigma_level}}σ divergence in {{metric}}.*

---

## 1 Macro & Sector Sensitivity (200-250 words)
- **Beta to SPY:** 20 / 60 / 250-day (Yahoo Finance)  
- **Top Macro Drivers:** CPI YoY (FRED CPIAUCSL), 10-yr UST (FRED DGS10)  
- **Economic Surprise Index:** {{esi_value}} (Citi public feed)  
- **Scenario Table:** GDP ±1 σ vs sector EPS growth (base / bull / bear)

## 2 Microstructure & Quant Signals (350-450 words)
### Data Inputs  
- Nasdaq TotalView (free prev-day file)  
- CBOE options “Trade Dump” CSV  
- FINRA Daily Short Volume  
- iShares ETF flow CSVs  

### Metrics & Formulas  
| Metric | Formula / Function | Look-back |
|--------|--------------------|-----------|
| Rolling β | `np.polyfit(ret_sector, ret_spy, 1)[0]` | 20 / 60 / 250 |
| RSI | `ta.rsi(close, n)` | 14 |
| Put/Call Skew | `puts_vol / calls_vol` | 5-day |

*Narrative:* comment on volume cliffs, liquidity pockets, gamma walls.

## 3 Fundamental Deep Dive (250-300 words)
- **TTM EPS vs FY-1 consensus:** {{eps_trend}}  
- **EV/EBITDA percentile:** {{ev_multiple}} vs 5-yr history  
- **Insider transactions (30 d):** net ${{insider_net}} (SEC EDGAR)  
- **Supply-chain heatmap:** Import Price Index + Baltic Dry rates

## 4 Technical Pattern Recognition (150-200 words)
- Price vs 50 / 200 DMA crossovers  
- VWAP deviations  
- High-probability candlestick clusters (≥ 70 % win-rate)

## 5 Risk & Position Sizing (150-200 words)
- **Kelly Fraction:** `edge / variance`  
- **Vol-Target Position:** `target_vol / sector_vol`  
- **Stop-loss:** 1.5 × ATR(14)

### Institutional Scalability
| Item | Value |
|------|-------|
| Sector ADV (USD) | {{adv}} |
| Trade Size @ 50 % ADV | {{impact_est}} bps (Almgren-Chriss) |

---

## 6 Company Deep Dives & Comparative Analytics (≈ 220 words each × {{num_companies}})
**Selection Method:** rank all {{sector_name}} constituents on  
40 % 3-yr Rev CAGR + 40 % ROIC + 20 % EV/EBITDA discount to 5-yr median.  
Top-{{num_companies}} move to deep-dive.

### Template (duplicate for each company)

#### {{company_name}} ({{ticker}})
| Metric | Current | 5-Yr Avg | Percentile vs Peers |
|--------|---------|---------|---------------------|
| Rev CAGR (3 y) | {{rev_cagr}} | {{rev_cagr_hist}} | {{rev_pctile}} |
| ROIC | {{roic}} | {{roic_hist}} | {{roic_pctile}} |
| Gross Margin | {{gm}} | {{gm_hist}} | {{gm_pctile}} |
| Net Debt / EBITDA | {{leverage}} | {{lev_hist}} | {{lev_pctile}} |
| EV/EBITDA | {{ev_ebitda}} | {{ev_hist}} | {{ev_pctile}} |
| Patent Filings (12 m) | {{patents}} | — | — |
| Google Trends Index | {{gt_score}} | — | — |

> **Narrative (≤ 120 words)**  
> • Moat: {{moat_point}}  
> • Pipeline & TAM: {{tam_point}}  
> • Mgmt sentiment delta: {{sentiment_stat}}  
> • Catalysts: {{catalyst_list}}  
> • Risks: {{risk_point}}

    # Quick-DCF (illustrative)
    fcf      = yahoo_fcf_growth('{{ticker}}', start='2019', end='{{date}}')
    wacc     = 0.09
    terminal = 0.025
    value    = dcf_model(fcf, wacc, terminal)

*DCF Implied Price:* **${{dcf_price}}** vs close **${{spot_price}}** ({{upside_pct}} %).  
*Implied IRR (95 % CI):* {{irr_ci}}

---

## 7 Cross-Company Heat-Map
| Factor | Best | Worst | Spread |
|--------|------|-------|--------|
| Rev CAGR | {{leader_cagr}} | {{lag_cagr}} | {{spread_cagr}} |
| ROIC | {{leader_roic}} | {{lag_roic}} | {{spread_roic}} |
| Valuation | {{cheapest}} | {{expensive}} | {{val_spread}} |
| Mgmt Sentiment | {{bullish_mgmt}} | {{bearish_mgmt}} | {{sent_spread}} |

---

## 8 Actionable Trades & Hedges (120-150 words)
1. **Long-Short Basket:** long {{long_basket}} / short {{short_basket}}, β-neutral, target α {{target_alpha}} bps/mo  
2. **Event-Driven Straddle:** {{event_ticker}} (implied vol {{impl_vol}} vs realised {{real_vol}}) into {{event_name}}

## 9 Performance Attribution (100-150 words)
- Expected Sharpe: {{sharpe}} (95 % CI {{sharpe_low}}–{{sharpe_high}})  
- Information Ratio vs {{benchmark_ticker}}: {{ir}}  
- Tracking Error: {{te}} bps annualised

---

## Output Formatting Rules
1. GitHub-flavoured Markdown; all section headers use `##`.  
2. Bullet lists ≤ 6 items; tables in pipe syntax only.  
3. Every numeric forecast **must** append “(95 % CI: x–y)”.  
4. Code blocks ≤ 15 lines; fence with four spaces or tildes inside Markdown.

---

## Validation Checklist *(hidden — LLM self-verify)*
- [ ] All `{{placeholders}}` replaced  
- [ ] ≥ 1 macro, 1 micro, **and** 1 company-level data source cited  
- [ ] Every forecast includes CI  
- [ ] Word-count limits met per section  
- [ ] Deep-dive tables generated for every company

---

## Example Invocation (abbrev.)
