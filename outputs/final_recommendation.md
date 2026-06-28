# Final Recommendation: Drivers of Monthly Sales Performance

**To:** Retail Chain Leadership  
**From:** Business Analytics  
**Date:** June 2026  
**Re:** Regression Analysis — Monthly Sales Drivers

---

## Executive Summary

A multiple regression model using data from 320 store-month observations (80 stores, Jan–Apr 2025) explains 83% of variation in monthly sales. **Footfall is by far the strongest driver**, followed by inventory availability and marketing spend. Leadership should prioritize actions that increase store traffic and ensure products are in stock when customers arrive.

---

## Which Factors Are Most Strongly Associated with Monthly Sales?

Based on regression analysis, ranked by statistical strength and business magnitude:

### 1. Footfall (Store Traffic) — Strongest Driver
- Simple regression R-squared: **0.7363** — footfall alone explains 74% of sales variance
- Multiple model coefficient: **+$34.00 per visitor per month**
- P-value: < 0.001 (extremely significant)
- **Implication:** Driving 1,000 more visitors per month to a store is associated with approximately $34,000 in additional monthly sales. This is the single most powerful lever available.

### 2. Inventory Availability
- Multiple model coefficient: **+$3,002 per 1% improvement**
- P-value: < 0.001 (highly significant)
- **Implication:** Moving from 80% to 85% inventory availability in a store is associated with ~$15,000 more in monthly sales. Out-of-stock situations are costing revenue.

### 3. Marketing Spend
- Multiple model coefficient: **+$1.20 per $1 spent**
- P-value: < 0.001 (highly significant)
- **Implication:** Marketing generates positive returns. A $50,000 monthly marketing investment is associated with roughly $60,000 in incremental sales — a positive but modest ROI that should be tracked against costs.

### 4. Customer Rating
- Multiple model coefficient: **+$13,630 per 1-point improvement**
- P-value: 0.005 (significant)
- **Implication:** Stores with higher customer satisfaction ratings generate more sales. This could reflect a virtuous cycle (better service → repeat visits → more sales), or shared drivers like staff quality.

### 5. Store Type and Region
- **Airport stores** (reference) generate the highest baseline sales vs all other types, particularly vs Residential (–$41,880)
- **South and West regions** outperform East by ~$18,000 per month, after controlling for other factors
- These are structural, not easily actionable — but matter for store investment prioritization

---

## Which Variables Should Leadership Focus On?

| Priority | Variable | Recommended Action |
|---|---|---|
| **Highest** | Footfall | Run footfall-driving campaigns (events, loyalty programs, local partnerships, social media targeting) |
| **High** | Inventory availability | Improve supply chain planning; set minimum availability thresholds of 90%+ |
| **Medium** | Marketing spend | Maintain or increase spend in high-footfall-potential markets; measure ROI per store |
| **Medium** | Customer rating | Invest in staff training and service standards; link rating to store management KPIs |

---

## Which Variables Should Not Be Over-Interpreted?

**avg_discount_pct:** The negative coefficient (–$45,710) is not statistically significant in the full model (p = 0.211). While it suggests higher discounts may not reliably increase sales, this result is inconclusive and may reflect that discounts are used reactively when stores are already underperforming. **Do not make discounting policy decisions based solely on this regression.**

**region_North** and **type_Mall:** Neither is statistically significant at the 5% level. Regional and format differences exist but may be explained by unobserved factors (store size, local demographics) rather than the region or format label itself.

**staff_count, holiday_flag, competitor_distance_km:** These were tested but did not significantly improve model performance and were excluded from the final model. They may have effects not captured by a 4-month dataset.

---

## Business Action Recommendations

1. **Launch a footfall-first campaign:** Given that traffic explains 74% of sales, even a 5–10% increase in monthly visitors across all stores would generate significant revenue. Focus on stores in the bottom quartile of footfall.

2. **Set inventory availability targets:** Implement a chain-wide minimum of 90% inventory availability. Based on the regression, each 1% point improvement is worth ~$3,000/store/month — at 80 stores, closing a 5% gap chain-wide is worth an estimated $1.2M+ per month.

3. **Redistribute marketing spend to high-potential stores:** Stores with high footfall potential but low marketing spend are under-served. Use the regression model to simulate expected sales uplift by store before budget decisions.

4. **Investigate Airport stores as a template:** Airport stores are the highest-performing format per the regression baseline. Understand what operational practices (product mix, staffing, layout) transfer to other store types.

5. **Prioritize South and West regions for expansion investment:** These regions show higher sales after controlling for other factors — suggesting favorable market conditions.

---

## Risks and Limitations

- **Correlation is not causation.** The model identifies associations; it cannot prove that increasing marketing spend or inventory will definitely increase sales. Controlled experiments (A/B tests) are needed to establish causal effects.
- **Only 4 months of data.** The dataset does not capture seasonal trends. A Christmas period, for example, could completely change the relative importance of factors.
- **Multicollinearity.** Footfall and marketing spend are likely correlated (marketing generates footfall). Individual coefficients may shift if the model's inputs change. The condition number is elevated (1.2×10⁶).
- **Missing variables.** Store size, lease cost, local competition density, product mix, and demographic data are not included. These could be material drivers not captured by the current model.
- **Residual patterns.** West region Mall and High Street stores are systematically over-predicted, suggesting the model does not fully capture their local dynamics.

---

## Why Regression Shows Association, Not Causation

Regression models observe patterns in existing data — they show that variables move together, but they cannot confirm that one causes the other. For example:
- Stores with higher marketing spend also have higher footfall and higher sales. This could mean marketing causes sales (via footfall), or it could mean that well-managed stores both spend more on marketing *and* happen to be in better locations.
- A store could increase its inventory availability from 80% to 95% and still not see the full $45,030 sales increase if the reason for low availability was unrelated to customer demand (e.g., supply chain disruption in products not typically purchased at that store).

To establish causation, the business should run controlled experiments — for example, randomly selecting stores to receive a marketing spend increase and comparing outcomes to control stores, or piloting inventory improvement in a subset of stores before rolling out chain-wide.

The regression analysis is the right starting point: it narrows the field of levers worth testing and provides quantitative magnitude estimates for business case building.
