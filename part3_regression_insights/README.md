# Part 3 — Regression Insights
**Business Scenario:** Retail chain leadership wants to understand which factors drive monthly store sales.

---

## Business Problem Summary

A retail chain with stores across 4 regions (East, North, South, West) and 4 store types (Airport, High Street, Mall, Residential) needs to know which operational and contextual factors most strongly predict monthly sales. Decisions to be made include: where to open new stores, how to allocate marketing budgets, whether to invest in staffing or inventory, and how to prioritise underperforming stores.

---

## Dataset Description

| Property | Detail |
|----------|--------|
| File | `business_regression_data.xlsx` |
| Records | 320 store-month observations |
| Stores | ~80 unique stores × 4 months (Jan–Apr 2025) |
| Regions | East, North, South, West |
| Store Types | Airport, High Street, Mall, Residential |
| Missing values | competitor_distance_km (6), customer_rating (8) — imputed with median |

---

## Variables

### Dependent Variable
- `monthly_sales` — Total sales revenue for a store in a given month (£)

### Independent Variables

| Variable | Type | Description |
|----------|------|-------------|
| marketing_spend | Numeric | Monthly marketing budget (£) |
| footfall | Numeric | Number of visitors per month |
| avg_discount_pct | Numeric | Average discount offered (0–1) |
| staff_count | Numeric | Number of staff in the store |
| inventory_availability_pct | Numeric | % of items in stock |
| competitor_distance_km | Numeric | Distance to nearest competitor (km) |
| holiday_flag | Binary (0/1) | Whether the month includes a public holiday |
| customer_rating | Numeric | Average customer satisfaction score (1–5) |
| region | Categorical → Dummies | East (ref), North, South, West |
| store_type | Categorical → Dummies | Airport (ref), High Street, Mall, Residential |

### Variables Not Used
- `store_id` — Identifier only, not a predictor
- `month` — Only 4 time points; insufficient for time series
- `monthly_profit` — Would be collinear with monthly_sales (both are outcomes)

---

## Regression Approach

1. Explored correlations between all numeric variables and `monthly_sales`
2. Ran 3 simple linear regressions (footfall, marketing_spend, staff_count)
3. Created dummy variables for region (ref: East) and store_type (ref: Airport)
4. Ran one multiple linear regression with all 7 numeric predictors + 6 dummies
5. Compared models using R², adjusted R², and p-values
6. Calculated residuals and identified over/under-performing stores
7. Wrote equations and business recommendations

---

## Dummy Variable Approach

Categorical variables cannot be used directly in regression. They are converted to binary (0/1) dummy columns.

- **Region**: 4 categories → 3 dummies (drop East as reference)
  - region_North, region_South, region_West
  - East = baseline (all three dummies = 0)
- **Store Type**: 4 categories → 3 dummies (drop Airport as reference)
  - store_High Street, store_Mall, store_Residential
  - Airport = baseline (all three dummies = 0)

Full explanation in `outputs/model_equations.md`.

---

## Model Comparison Summary

| Model | Predictor(s) | R² | Verdict |
|-------|-------------|-----|---------|
| SLR 1 | footfall | 0.7363 | Strong baseline |
| SLR 2 | marketing_spend | 0.1672 | Weakest model |
| SLR 3 | staff_count | 0.6523 | Strong single predictor |
| **MLR** | All 8 numeric + 6 dummies | **0.8411** | **Best model** |

---

## Final Model Selected

**Multiple Linear Regression** — R² = 0.8411
, Adjusted R² = 0.8338

Explains 84.1% of monthly sales variation. All major predictors statistically significant at p < 0.05 except region_North, Store High Street, Store Mall and avg_discount_pct.

---

## Business Recommendation

1. **Drive footfall** — strongest predictor (+£27.89 per visitor)
2. **Prioritise Airport/Mall locations** — Residential stores earn £42,015/month less
3. **Improve inventory availability** — each 1% gain → +£3,112 in sales
4. **Invest in customer experience** — each 1-star rating gain → +£13,389 in sales
5. **Target marketing at low-footfall stores** — £1.17 return per £1 spent
6. **Do not over-interpret discount %** — not statistically significant in model

Full recommendation in `outputs/final_recommendation.md`.

---

## Assumptions and Limitations

- Relationships are assumed to be linear
- Missing values imputed with median (minor impact)
- Only 4 months of data — seasonal trends not fully captured
- Regression shows association, NOT causation — A/B tests needed before major investment
- Multicollinearity exists between footfall and staff_count

---

## Screenshots Included

| File | Description |
|------|-------------|
| `screenshots/simple_regression_output.png` | SLR 1 (footfall) output table |
| `screenshots/multiple_regression_output.png` | Full MLR coefficient table |
| `screenshots/residuals_preview.png` | Predicted vs actual sales with residuals |
| `screenshots/model_comparison_preview.png` | Side-by-side model comparison table |
