# Model Comparison

## Overview

Three regression models were built and compared to understand drivers of monthly sales at a retail chain.

---

## Model 1: Simple Regression — Footfall

**Model Name:** Simple Regression (Footfall)  
**Dependent Variable:** monthly_sales  
**Independent Variable:** footfall  

**Regression Equation:**
```
monthly_sales = 446,411 + 35.678 × footfall
```

| Metric | Value |
|---|---|
| R-squared | 0.7363 |
| Coefficient (footfall) | 35.678 |
| P-value | < 0.001 |
| Intercept | 446,410.58 |

**Significant Variables:** footfall (highly significant, p < 0.001)

**Business Usefulness:** This is the strongest single-variable predictor. More than 73% of sales variance is explained by footfall alone. This is highly actionable: store traffic is a primary lever.

**Limitations:** Does not capture the effect of marketing, inventory, discounting, or store type. Cannot be used to evaluate the ROI of specific spend decisions.

---

## Model 2: Simple Regression — Marketing Spend

**Model Name:** Simple Regression (Marketing Spend)  
**Dependent Variable:** monthly_sales  
**Independent Variable:** marketing_spend  

**Regression Equation:**
```
monthly_sales = 560,777 + 2.130 × marketing_spend
```

| Metric | Value |
|---|---|
| R-squared | 0.1672 |
| Coefficient (marketing_spend) | 2.130 |
| P-value | < 0.001 |
| Intercept | 560,777.35 |

**Significant Variables:** marketing_spend (significant, p < 0.001)

**Business Usefulness:** Confirms marketing spend has a statistically significant positive association with sales. However, it explains only 17% of variance, meaning marketing is one factor among many. ROI at $2.13 per dollar spent is useful for budget planning.

**Limitations:** Marketing may be endogenously related to footfall (higher spend → more footfall → more sales). The bivariate relationship may overstate marketing's independent impact.

---

## Model 3: Multiple Regression (Final Model)

**Model Name:** Multiple Regression — All Key Predictors  
**Dependent Variable:** monthly_sales  
**Independent Variables:** marketing_spend, footfall, inventory_availability_pct, avg_discount_pct, customer_rating, region dummies (North, South, West vs East), store type dummies (High Street, Mall, Residential vs Airport)

**Regression Equation:**
```
monthly_sales = 91,790
  + 1.200 × marketing_spend
  + 34.003 × footfall
  + 3,001.99 × inventory_availability_pct
  - 45,710 × avg_discount_pct
  + 13,630 × customer_rating
  + 6,185 × region_North
  + 18,690 × region_South
  + 18,110 × region_West
  - 23,790 × type_High Street
  - 12,790 × type_Mall
  - 41,880 × type_Residential
```

| Metric | Value |
|---|---|
| R-squared | 0.8320 |
| Adjusted R-squared | 0.8260 |
| F-statistic | 138.7 |
| F-statistic p-value | < 0.001 |

**Significant Variables (p < 0.05):**
- footfall (p < 0.001)
- marketing_spend (p < 0.001)
- inventory_availability_pct (p < 0.001)
- customer_rating (p = 0.005)
- region_South (p = 0.009)
- region_West (p = 0.004)
- type_High Street (p = 0.011)
- type_Residential (p < 0.001)

**Not significant (p > 0.05):**
- avg_discount_pct (p = 0.211) — directionally negative but not conclusive
- region_North (p = 0.380)
- type_Mall (p = 0.187)

**Business Usefulness:** The final model explains 83% of sales variance. It allows leadership to quantify the independent contribution of each factor after controlling for others — much more reliable than simple regressions for multi-factor decision-making.

**Limitations:**
- High condition number suggests multicollinearity; individual coefficients should be interpreted cautiously
- Assumes linear relationships; non-linear effects are not captured
- Only 4 months of data; seasonal patterns may bias some estimates
- Omits store size, local demographics, and competitor behavior

---

## Comparison Table

| Model | R-squared | Adj R-sq | Key Significant Vars | Best Use Case |
|---|---|---|---|---|
| Simple: Footfall | 0.7363 | 0.7352 | footfall | Quick summary; traffic-focused decisions |
| Simple: Marketing Spend | 0.1672 | 0.1645 | marketing_spend | Marketing ROI estimation only |
| Multiple (Final) | 0.8320 | 0.8260 | footfall, marketing, inventory, rating, region, type | Full multi-factor business analysis |

**Selected Final Model:** Multiple Regression (R-squared = 0.832)

The multiple regression model is selected as the final model because it:
1. Explains the most variance (83%)
2. Controls for confounding between variables
3. Allows simultaneous evaluation of multiple business levers
4. Provides actionable coefficients for footfall, marketing, and inventory
