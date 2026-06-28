## Models Built

### Model 1 — SLR: footfall
- **Type:** Simple Linear Regression
- **Variables:** monthly_sales ~ footfall
- **R-squared:** 0.7363
- **Coefficient:** 35.6780 (each extra visitor → +£35.68 in sales)
- **P-value:** < 0.000001 (highly significant)
- **Equation:** Sales = 446,410 + 35.68 × footfall
- **Business usefulness:** Strong. Footfall alone explains 73.6% of sales variation. Useful for quick store performance estimates and footfall-driving decisions (location, hours, promotions).
- **Limitations:** Ignores marketing spend, inventory, discounting, store type, and region. Over-simplified for real business decisions.

---

### Model 2 — SLR: marketing_spend
- **Type:** Simple Linear Regression
- **Variables:** monthly_sales ~ marketing_spend
- **R-squared:** 0.1672
- **Coefficient:** 2.1296 (each £1 of marketing → +£2.13 in sales)
- **P-value:** < 0.000001 (significant)
- **Equation:** Sales = 560,777 + 2.13 × marketing_spend
- **Business usefulness:** Moderate. Shows a positive return on marketing (£2.13 per £1 spent), but R² is very low — marketing alone explains only 16.7% of sales. Many other factors dominate.
- **Limitations:** Weakest model. Correlation may be partly driven by confounding — larger or busier stores both spend more on marketing AND have higher sales.

---

### Model 3 — SLR: staff_count
- **Type:** Simple Linear Regression
- **Variables:** monthly_sales ~ staff_count
- **R-squared:** 0.6523
- **Coefficient:** 16,984 (each additional staff member → +£16,984 in sales)
- **P-value:** < 0.000001 (highly significant)
- **Equation:** Sales = 400,551 + 16,984 × staff_count
- **Business usefulness:** High. Staff count is a strong predictor, likely because larger/busier stores need more staff AND generate more sales. Useful for workforce planning.
- **Limitations:** Causation unclear — are more staff driving sales, or do high-sales stores hire more staff? Collinear with footfall (r ≈ 0.78).

---

### Model 4 — Multiple Linear Regression (FINAL MODEL)
- **Type:** Multiple Linear Regression
- **Variables:** monthly_sales ~ marketing_spend + footfall + inventory_availability_pct + avg_discount_pct + customer_rating + staff_count + holiday_flag + region dummies (North, South, West vs East) + store type dummies (High Street, Mall, Residential vs Airport)
- **R-squared:** 0.8410
- **Adjusted R-squared:** 0.8337
- **F-statistic p-value:** < 0.000001 (entire model highly significant)
- **Business usefulness:** Highest. Explains 84.1% of sales variation and separates the effect of each factor while controlling for others. The only model suitable for business decision-making.
- **Limitations:** Cannot prove causation. Missing external factors (local economy, weather, nearby events). Some multicollinearity between footfall and staff_count.

---

## Head-to-Head Comparison

| Criterion             | SLR 1: Footfall | SLR 2: Marketing | SLR 3: Staff | Multiple Regression |
|-----------------------|-----------------|------------------|--------------|---------------------|
| R-squared             | 0.7363          | 0.1672           | 0.6523       | **0.8410**          |
| Adjusted R-squared    | —               | —                | —            | **0.8337**          |
| Dummy variables       | No              | No               | No           | **Yes**             |
| Controls for confounders | No           | No               | No           | **Yes**             |
| No. of predictors     | 1               | 1                | 1            | 13                  |
| Best for              | Quick estimate  | ROI check        | HR planning  | **All decisions**   |
| Verdict               | Good baseline   | Weakest model    | Strong model | **BEST MODEL**      |

---

## Why the Multiple Regression Wins

1. **Higher R²**: Explains 84.1% of sales variance vs 73.6% for the best simple model
2. **Controls for confounders**: In SLR, staff_count looks very strong partly because busy stores hire more staff. MLR separates this effect.
3. **Includes store and region context**: A Residential store in the North is very different from an Airport store in the West — SLR models can't capture this.
4. **More actionable**: Gives individual coefficients for each lever leadership can pull (marketing budget, inventory investment, staffing levels).

---

## Significant Variables Summary (Multiple Regression)

| Variable | P-value | Significant? |
|----------|---------|--------------|
| footfall | < 0.001 | Yes *** |
| marketing_spend | < 0.001 | Yes *** |
| inventory_availability_pct | < 0.001 | Yes *** |
| customer_rating | 0.0049 | Yes ** |
| staff_count | 0.0102 | Yes * |
| holiday_flag | 0.0242 | Yes * |
| region_South | 0.0059 | Yes ** |
| region_West | 0.0020 | Yes ** |
| store_Residential | < 0.001 | Yes *** |
| store_High Street | 0.4594 | **No** |
| avg_discount_pct | 0.1599 | **No** |
| region_North | 0.87632 | **No** |
| store_Mall | 0.9466 | **No** |
