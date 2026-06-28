# Residual Analysis

## Model Used

**Final Multiple Regression Model**  
Dependent variable: monthly_sales  
R-squared: 0.832

Residual = Actual monthly_sales − Predicted monthly_sales

A positive residual means the store performed **better** than the model predicted (given its footfall, marketing spend, inventory, etc.)  
A negative residual means the store performed **worse** than the model predicted.

---

## Top 5 Records with Largest Positive Residuals (Model Under-Predicted)

| Store ID | Region | Store Type | Actual Sales ($) | Predicted Sales ($) | Residual ($) |
|---|---|---|---|---|---|
| STR-1028 | East | Residential | 713,611.16 | 600,860.03 | +112,751.13 |
| STR-1073 | East | Residential | 813,316.71 | 707,149.99 | +106,166.71 |
| STR-1019 | East | Residential | 788,087.68 | 695,490.42 | +92,597.26 |
| STR-1069 | West | Residential | 686,737.87 | 595,017.79 | +91,720.08 |
| STR-1050 | North | Residential | 735,786.64 | 646,314.27 | +89,472.37 |

**Business Interpretation:**  
These stores are consistently outperforming model expectations. All five are **Residential** store types. The model assigns a large negative coefficient to Residential stores (–$41,880 vs Airport stores), yet these particular stores are exceeding predictions by $90,000–$113,000. This suggests there may be local micro-market advantages (high-density residential catchment, limited competition, community loyalty) that the model's store-type dummy cannot fully capture. These stores represent best-practice examples worth investigating.

---

## Top 5 Records with Largest Negative Residuals (Model Over-Predicted)

| Store ID | Region | Store Type | Actual Sales ($) | Predicted Sales ($) | Residual ($) |
|---|---|---|---|---|---|
| STR-1017 | West | High Street | 685,379.08 | 844,891.98 | –159,512.90 |
| STR-1023 | South | Mall | 627,171.90 | 773,115.05 | –145,943.15 |
| STR-1012 | West | Residential | 595,467.60 | 715,299.08 | –119,831.48 |
| STR-1007 | West | Mall | 800,451.94 | 913,150.73 | –112,698.79 |
| STR-1014 | West | High Street | 463,534.25 | 563,492.79 | –99,958.54 |

**Business Interpretation:**  
These stores are significantly underperforming against model expectations given their observable inputs (traffic, marketing, inventory). Notable patterns:
- **West region** appears in 4 of 5 cases, suggesting the West region coefficient may not fully capture local headwinds (higher competition, consumer preferences, or economic factors)
- **Mall and High Street** stores dominate the negative outliers, consistent with broader retail trends of declining foot traffic in these formats
- STR-1017 and STR-1014 (both High Street, West) have very large negative residuals, warranting direct operational review

---

## Under-Prediction vs Over-Prediction by Segment

| Segment | Pattern |
|---|---|
| Residential stores | Model systematically under-predicts (positive residuals dominant) |
| West region — Mall/High Street | Model systematically over-predicts (negative residuals dominant) |
| Airport stores (reference) | Residuals are more balanced — model is calibrated to this type |

---

## Overall Residual Diagnostics

- The model's residuals have moderate skewness (–0.27), with slight left tail — some stores significantly below prediction
- Durbin-Watson statistic = 2.094 — no strong serial autocorrelation
- Prob(Omnibus) = 0.020 — mild deviation from normality; large sample mitigates concern
- Residual standard error is approximately $42,000 — meaning typical predictions are within ±$42K of actual sales

---

## Implications for Business Decisions

1. **Do not apply the model's predictions uniformly.** Stores in the West — particularly Mall and High Street formats — should have predictions discounted by at least $50–$100K.
2. **Residential stores in East and North regions** may have untapped growth potential if they are consistently outperforming model benchmarks.
3. **Investigate STR-1017 and STR-1023** specifically — their gaps are large enough to warrant operational audits (lease costs, local events, staffing issues, competition).
