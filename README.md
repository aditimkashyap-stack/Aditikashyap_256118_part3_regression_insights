
# Part 3: Regression-Based Business Insights & Model Interpretation

## Business Problem Summary

A retail chain with 80 stores across four regions wants to understand what drives monthly sales performance. Leadership is considering actions such as increasing marketing spend, improving inventory, adjusting discounting strategy, and reallocating staff. This analysis uses linear regression to identify which factors are most strongly associated with monthly sales and provides data-backed recommendations.

---

## Dataset Description

**File:** `data/business_regression_data.xlsx`  
**Rows:** 320 observations (80 stores × 4 months: Jan–Apr 2025)  
**Columns:** 14

| Column | Type | Role |
|---|---|---|
| store_id | Categorical | Identifier — not used in regression |
| month | Date | Temporal variable — not used directly |
| region | Categorical | Independent — converted to dummies |
| store_type | Categorical | Independent — converted to dummies |
| marketing_spend | Numeric | Independent variable |
| footfall | Numeric | Independent variable |
| avg_discount_pct | Numeric | Independent variable |
| staff_count | Numeric | Independent — excluded (no significant effect) |
| inventory_availability_pct | Numeric | Independent variable |
| competitor_distance_km | Numeric | Independent — 6 missing values, imputed with median |
| holiday_flag | Binary (0/1) | Independent — tested; not significant in final model |
| customer_rating | Numeric | Independent variable (8 missing, imputed) |
| **monthly_sales** | **Numeric** | **Dependent variable (Y)** |
| monthly_profit | Numeric | Excluded — downstream outcome of sales, not a driver |

---

## Dependent and Independent Variables

**Dependent Variable (Y):** `monthly_sales`

**Independent Variables Used in Final Model:**
- `marketing_spend` (numeric)
- `footfall` (numeric)
- `inventory_availability_pct` (numeric)
- `avg_discount_pct` (numeric)
- `customer_rating` (numeric)
- Region dummies: `region_North`, `region_South`, `region_West` (reference: East)
- Store type dummies: `type_High Street`, `type_Mall`, `type_Residential` (reference: Airport)

**Variables Excluded from Final Model:**
- `store_id`, `month` — identifiers/time labels
- `monthly_profit` — outcome, not a driver
- `staff_count` — not statistically significant in preliminary tests
- `holiday_flag` — not significant in multiple regression
- `competitor_distance_km` — weak/inconsistent relationship

---

## Regression Approach

1. Data cleaning: imputed 6 missing `competitor_distance_km` values and 8 missing `customer_rating` values with column medians
2. Created dummy variables for `region` (reference: East) and `store_type` (reference: Airport)
3. Ran 5 simple linear regressions to identify individually significant variables
4. Ran one multiple regression combining the strongest predictors plus dummy variables
5. Calculated predicted values and residuals for the final model
6. Compared model performance by R-squared, significance, and business usefulness

---

## Dummy Variable Approach

**Region dummies** (reference category: **East**):
- `region_North`, `region_South`, `region_West`

**Store type dummies** (reference category: **Airport**):
- `type_High Street`, `type_Mall`, `type_Residential`

The reference category is omitted to avoid perfect multicollinearity (the dummy variable trap). Coefficients on dummies represent the sales difference vs. the reference category, holding all else constant.

---

## Model Comparison Summary

| Model | Variables | R-squared | Best use |
|---|---|---|---|
| Simple 1: Footfall | footfall | 0.7363 | Strong single predictor |
| Simple 2: Marketing Spend | marketing_spend | 0.1672 | Directional insight only |
| Multiple (Final) | All 5 numeric + 6 dummies | 0.8320 | Best overall explanatory power |

---

## Final Model Selected

**Multiple Regression Model** — R-squared = 0.832

Equation:
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

---

## Business Recommendation

**Top priority lever:** Increase footfall — each additional visitor is associated with ~$34 in monthly sales, and footfall alone explains 74% of sales variance.

**Second priority:** Improve inventory availability — each 1% improvement is associated with ~$3,002 additional sales per month, and the effect is statistically significant.

**Third:** Increase marketing spend — significant positive effect ($1.20 per dollar spent), but ROI should be monitored.

**Caution:** Discounting is negatively associated with sales, suggesting higher discounts do not drive volume reliably in this dataset. Customer rating has a positive and significant effect in the multiple model.

**Do not over-interpret:** Region and store type differences exist but may reflect structural factors (store size, catchment area) not actionable through short-term campaigns.

---

## Assumptions and Limitations

- OLS assumes linearity, homoscedasticity, no perfect multicollinearity, and normally distributed residuals
- High condition number (1.2×10⁶) signals some multicollinearity — coefficients should be interpreted with caution
- Only 4 months of data — seasonal variation is not fully captured
- Regression shows association, not causation; confounding variables (store size, local competition, economic conditions) are not included
- 80 stores — results may not generalize to new store types or markets

---

## Screenshots Included

| File | Shows |
|---|---|
| `screenshots/simple_regression_output.png` | Footfall simple regression output |
| `screenshots/multiple_regression_output.png` | Full multiple regression output |
| `screenshots/residuals_preview.png` | Predicted values, actuals, and residuals |
| `screenshots/model_comparison_preview.png` | Side-by-side model comparison table |
