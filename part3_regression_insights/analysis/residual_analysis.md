# Residual Analysis — Multiple Regression Model
**Model:** monthly_sales ~ footfall + marketing_spend + inventory_availability_pct + avg_discount_pct + customer_rating + staff_count + holiday_flag + region dummies + store type dummies  
**Formula:** Residual = Actual Sales − Predicted Sales

A positive residual means the store sold MORE than the model predicted.  
A negative residual means the store sold LESS than the model predicted.

---

## Top 5 Positive Residuals (Model Under-Predicted)

| Store ID | Region | Store Type | Actual Sales | Predicted Sales | Residual |
|----------|--------|------------|-------------|-----------------|----------|
| STR-1028 | East | Mall | £713,611 | £600,329 | **+£113,283** |
| STR-1030 | West | Residential | £820,519 | £726,530 | **+£93,989** |
| STR-1073 | East | Residential | £813,317 | £721,906 | **+£91,411** |
| STR-1026 | East | Mall | £625,514 | £534,473 | **+£91,041** |
| STR-1051 | East | Airport | £787,716 | £698,277 | **+£89,438** |

### Business Interpretation — Positive Residuals

These stores are **outperforming** what the model expects given their footfall, marketing spend, inventory, and other measured factors. Possible explanations:

- **Unmeasured local advantage**: Nearby major employer, popular neighbourhood, or unique product assortment not captured in the data.
- **Strong store management**: Exceptional staff quality, customer service, or in-store experience that the `customer_rating` column doesn't fully capture.
- **STR-1028 and STR-1026 (East Mall)**: Both Mall stores in the East region are over-performing. This could signal that East Mall locations benefit from specific tenant mix or catchment area advantages worth investigating.
- **STR-1030 and STR-1073 (Residential)**: Residential stores typically underperform (store_Residential dummy = −£42,015), yet these two beat the model significantly — they may serve dense, high-income residential areas.

**Recommendation:** Visit these stores to identify best practices that could be replicated elsewhere.

---

## Top 5 Negative Residuals (Model Over-Predicted)

| Store ID | Region | Store Type | Actual Sales | Predicted Sales | Residual |
|----------|--------|------------|-------------|-----------------|----------|
| STR-1017 | West | High Street | £685,379 | £851,815 | **−£166,436** |
| STR-1023 | South | Mall | £627,172 | £762,462 | **−£135,290** |
| STR-1012 | West | Residential | £595,468 | £721,540 | **−£126,072** |
| STR-1007 | West | Mall | £800,452 | £911,633 | **−£111,181** |
| STR-1014 | West | High Street | £463,534 | £558,407 | **−£94,873** |

### Business Interpretation — Negative Residuals

These stores are **under-performing** relative to what the model predicts. Despite having the footfall, marketing spend, and inventory levels that should drive higher sales, they are falling short. Possible explanations:

- **West region concentration**: Four of the five under-performers are in the West region, despite West having a positive regional dummy (+£19,258 vs East on average). This suggests West has high variance — some stores do very well, others significantly underperform.
- **STR-1017 and STR-1014 (West High Street)**: Both High Street stores in West are badly under-performing. High Street stores already carry a −£22,608 penalty in the model, yet these two fall even further below. Local competition or poor footfall-to-conversion rates may be the issue.
- **STR-1023 (South Mall)**: A Mall store in South under-performing significantly. Could indicate this particular mall has low footfall quality (visitors who browse but don't buy).
- **Possible data issue**: Large negative residuals can also flag data entry errors or one-off events (store closure, refurbishment) not captured in the dataset.

**Recommendation:** Prioritise operational review of these five stores. Investigate competitor activity, local demographics, and conversion rates.

---

## Are There Systematic Patterns in the Residuals?

### By Store Type
- **Residential stores** show the highest residual variance — the model struggles most with this type. This is expected because residential neighbourhoods vary enormously in income, density, and demographics.
- **Airport stores** have tighter residuals — performance is more predictable, likely because airport footfall is more consistent and conversion rates are more uniform.

### By Region
- **West region** has the most negative residuals among under-performers (4 of 5 worst). Leadership should investigate whether West stores face structural challenges the model isn't capturing (e.g. stronger local competition, different customer behaviour).
- **East region** dominates positive residuals (3 of 5 best), suggesting East has hidden advantages beyond what the model measures.

---

## Model Accuracy Assessment

- **R-squared = 0.8380**: The model explains 83.8% of sales variation — strong for real-world business data.
- **Largest residual**: £166,436 on a store with £685,379 in actual sales ≈ 24.3% error.
- **Most residuals** fall within ±£80,000, which is reasonable given sales range from £400,831 to £946,834.
- **The model does NOT systematically over- or under-predict** across all stores — residuals are roughly centred around zero, which is healthy.

---

## Limitations of Residual Analysis

1. Residuals may reflect genuine business factors the model can't see (local competition, economic conditions, store management quality).
2. Some large residuals may be one-off events (promotions, refurbishments, weather events) not captured in the dataset.
3. With only 4 months of data per store, some residuals may reflect seasonal patterns not yet fully modelled.
