# 🛒 Superstore Profitability Dashboard

A profitability diagnostic on the public **Sample Superstore** dataset (9,994 order lines · 5,009 orders · 2014–2017), built as a **2-page Power BI dashboard** and replicated **chart-for-chart in Python** (pandas + matplotlib) so the analysis is fully reproducible — then extended with a **prescriptive scenario layer** that quantifies the recommended fix.

> **The question:** Superstore is profitable overall — so where is it *quietly losing money*?

---

## 🔑 Headline finding

| Metric | Value |
|---|---|
| Revenue | **$2.30M** |
| Total Profit | **$286K** |
| Margin | **12.47%** |
| Avg Discount | 15.62% |
| **Loss rate (line items)** | **18.72%** |
| Orders | 5,009 |

The company is profitable **on average**, yet **nearly 1 in 5 line items is sold at a loss** — the winners are subsidising a large pool of losers. This project finds the losers and quantifies the fix.

---

## 📊 The dashboard

### Page 1 — Sale Dashboard *(descriptive: "what does the business look like?")*
- **KPI cards** — revenue, profit, margin, discount, loss %, orders
- **Sales & Profit by Year** — sales +52%, profit +89% (2014→2017), but loss rate stays flat at ~18.7% → growth sits *on top of* a stable leak
- **Sales by Year & Month** — a repeating **Q4 peak / February trough** every year
- **By Segment** — Consumer biggest by sales ($1.16M) but worst margin (11.6%); Home Office smallest yet best (14.0%)
- **By Region** — Central runs **7.9%** margin, roughly **half** of the West (14.9%)
- **By Category** — Technology 17.4% & Office Supplies 17.0%, but **Furniture just 2.5%** (first red flag)

### Page 2 — Profitability & Discount Analysis *(diagnostic: "where & why is profit destroyed?")*
- **Average Profit by Discount Bucket** — positive ≤20%, negative in every bucket above (low of –$299 at 41–50%)
- **Loss-Rate by Discount Bucket** — the key chart: loss rate jumps **14% → 91.6%** crossing 20%, and hits **100% above 40%**
- **Sales by Sub-Category** — top sellers: Phones, Chairs, Storage, **Tables**, Binders
- **Profit by Sub-Category** — **Tables is the worst at –$17.7K** despite being a top-4 seller; **Copiers the best at +$55K** on protected pricing

### Prescriptive extension — quantifying the fix
- **4 Pillars of Data Analytics coverage matrix** — each chart mapped against Descriptive / Diagnostic / Predictive / Prescriptive (pillars a chart cannot honestly support are marked *skipped*, not padded)
- **Discount-Cap Waterfall** — *Current $286K + Avoided Losses $135K = After Cap $421K*. The +$135K uplift (+47%) is the dollar value of Recommendation #1.
- **Sub-Category × Discount split** — does the 20% cap fix each loss-maker? Tables ✓, Bookcases ✓, **Supplies ✗** (no orders above 20% — its leak is elsewhere)
- **Supplies drill-down (0–10% vs 11–20%)** — reveals Supplies *is* discount-sensitive, just at a tighter threshold: +$1,718 at 0–10%, –$2,907 at 11–20%. A ≈10% cap on Supplies recovers the full loss.

---

## 💡 Recommendations

| # | Recommendation | Evidence | Estimated impact |
|---|---|---|---|
| 1 | **Cap discretionary discounts at 20%** — system-block deeper discounts; require manager approval to override. | Loss Rate by Discount Bucket; Discount-Cap Waterfall | **≈ +$135K** (~+47% uplift) |
| 2 | **Re-cost or discontinue Tables** | Sub-Category Profit | *Mostly already captured by #1* — Tables' >20% losses (–$30.7K) are inside the cap uplift. |
| 3 | **Protect Copiers' pricing** — no volume discounts | Sub-Category Profit | *Defensive, no marginal $* — keeps existing +$55K intact. |
| 4 | **Apply a tighter sub-category cap (≈10%) to Supplies** | Supplies 0–10% vs 11–20% drill-down | **≈ +$1.2K** (full Supplies loss recovered) |
| 5 | **Pre-stock Q4 inventory and staffing** | Monthly Sales | Operational — reduces stockout risk in peak months |

**One-line conclusion:** The leak isn't a category problem or a region problem — it's a **discount-discipline** problem. One pricing rule (cap at 20%, with a tighter ≈10% for Supplies) recovers ≈ +$136K of annual profit without changing the product mix, the segment mix, or the sales target.
