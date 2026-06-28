# Model Equations

## Simple Regression Equations

### Model 1: Footfall → Monthly Sales

```
monthly_sales = 446,411 + 35.678 × footfall
```

**Interpretation:** For every additional customer who visits the store in a month, monthly sales increase by approximately $35.68, holding all else constant. A store going from 8,000 to 9,000 monthly visitors would be expected to gain roughly $35,678 in sales.

**R-squared: 0.7363** — Footfall alone explains 73.6% of variation in monthly sales.

---

### Model 2: Marketing Spend → Monthly Sales

```
monthly_sales = 560,777 + 2.130 × marketing_spend
```

**Interpretation:** For every additional $1 spent on marketing in a month, monthly sales increase by approximately $2.13. A store increasing its monthly marketing budget by $10,000 would be expected to gain about $21,300 in sales.

**R-squared: 0.1672** — Marketing spend alone explains 16.7% of sales variation — useful but not the dominant driver.

---

## Multiple Regression Equation (Final Model)

```
monthly_sales = 91,790
  + 1.200  × marketing_spend
  + 34.003 × footfall
  + 3,001.99 × inventory_availability_pct
  - 45,710  × avg_discount_pct
  + 13,630  × customer_rating
  + 6,185   × region_North
  + 18,690  × region_South
  + 18,110  × region_West
  - 23,790  × type_High Street
  - 12,790  × type_Mall
  - 41,880  × type_Residential
```

**R-squared: 0.832** — This model explains 83.2% of variation in monthly sales.

---

## Explanation of Each Coefficient

| Variable | Coefficient | P-value | Interpretation |
|---|---|---|---|
| Intercept | 91,790 | 0.055 | Baseline expected sales for an Airport store in East region, with all numeric predictors at zero (theoretical baseline only) |
| marketing_spend | +1.200 | <0.001 | Each $1 of marketing spend is associated with $1.20 in additional sales (after controlling for other factors) |
| footfall | +34.003 | <0.001 | Each additional monthly visitor is associated with $34.00 in additional sales |
| inventory_availability_pct | +3,001.99 | <0.001 | Each 1 percentage point improvement in inventory availability is associated with $3,002 additional monthly sales |
| avg_discount_pct | -45,710 | 0.211 | Higher discounting is negatively associated with sales, but this effect is not statistically conclusive in the full model |
| customer_rating | +13,630 | 0.005 | Each 1-point improvement in customer rating (e.g., from 3.0 to 4.0) is associated with $13,630 additional monthly sales |
| region_North | +6,185 | 0.380 | North stores average $6,185 more than East (reference), but this is not statistically significant |
| region_South | +18,690 | 0.009 | South stores average $18,690 more than East stores, after controlling for other factors |
| region_West | +18,110 | 0.004 | West stores average $18,110 more than East stores, after controlling for other factors |
| type_High Street | -23,790 | 0.011 | High Street stores average $23,790 less than Airport stores (reference) |
| type_Mall | -12,790 | 0.187 | Mall stores average $12,790 less than Airport stores, but this is not statistically conclusive |
| type_Residential | -41,880 | <0.001 | Residential stores average $41,880 less than Airport stores |

---

## Dummy Variable Explanation

Categorical variables cannot be used directly in regression — they must be converted to binary (0/1) dummy variables.

**Region:** Four categories (East, North, South, West)  
**Reference category:** East  
**Dummies created:** region_North, region_South, region_West  
When a store is in the East, all three dummies = 0, so the intercept captures the East baseline.  
When region_North = 1, the model adds $6,185 to the prediction (on top of the East baseline).

**Store Type:** Four categories (Airport, High Street, Mall, Residential)  
**Reference category:** Airport  
**Dummies created:** type_High Street, type_Mall, type_Residential  
Airport stores are the reference (all type dummies = 0). Airport stores are typically premium-capture locations with high footfall and captive audiences — making them a natural high-sales baseline.

**Why one category is omitted:** Including all categories would create perfect multicollinearity (the "dummy variable trap"), making the model impossible to solve. The reference category's effect is embedded in the intercept.

---

## Final Model Selected

**Multiple Regression** is the final model.

**Reason:** It achieves the highest explanatory power (R-squared = 0.832) and controls for the simultaneous effects of multiple business levers. Unlike simple regressions, it isolates the independent contribution of each factor — e.g., showing that marketing spend has a positive effect even after accounting for footfall, which it partly generates. This multi-factor view is essential for business decision-making, where managers must choose how to allocate limited budgets across marketing, inventory, and operational improvements.
