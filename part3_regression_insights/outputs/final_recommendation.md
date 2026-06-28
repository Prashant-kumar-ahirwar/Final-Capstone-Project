# Final Recommendation Memo
**To:** Retail Chain Leadership Team  
**From:** Business Analyst  
**Re:** Sales Driver Analysis — Regression Findings & Recommendations

---

## 1. Which Factors Are Most Strongly Associated with Monthly Sales?

Based on the multiple regression model (R² = 0.8380), the following factors show the strongest and most statistically reliable associations with monthly sales:

| Rank | Factor | Effect per Unit | Significance |
|------|--------|----------------|--------------|
| 1 | Footfall (monthly visitors) | +£27.89 per visitor | *** Very High |
| 2 | Store type: Residential vs Airport | −£42,015 | *** Very High |
| 3 | Marketing spend | +£1.17 per £1 spent | *** Very High |
| 4 | Inventory availability | +£3,112 per 1% improvement | *** Very High |
| 5 | Customer rating | +£13,389 per 1-star improvement | ** High |
| 6 | Staff count | +£3,188 per staff member | * Moderate |
| 7 | Holiday month | +£14,744 vs non-holiday | * Moderate |
| 8 | Region (South/West vs East) | +£19,000–£19,500 | ** High |

---

## 2. Which Variables Should Leadership Focus On?

### Priority 1 — Drive Footfall (Highest Impact)
Footfall is the single strongest driver of sales in both the simple model (R²=0.7363) and the multiple model. Every additional visitor is worth £27.89 in monthly sales.

**Recommended actions:**
- Invest in footfall-driving strategies: extended opening hours, loyalty schemes, events, and local partnerships
- Prioritise high-footfall locations when opening new stores
- Monitor footfall weekly as a leading indicator of monthly sales

### Priority 2 — Optimise Store Type Mix
The store type coefficients reveal a clear performance hierarchy:
- Airport stores are the strongest performers (reference baseline)
- High Street stores earn £22,608 less per month than Airport equivalents
- Residential stores earn £42,015 less per month than Airport equivalents

**Recommended actions:**
- When evaluating new store locations, strongly favour Airport and Mall sites over Residential
- For existing Residential stores that are under-performing, evaluate whether operational improvements can close the gap or whether they should be restructured

### Priority 3 — Improve Inventory Availability
Each 1 percentage point improvement in inventory availability is associated with £3,112 more in monthly sales. This is directly actionable through better supply chain management.

**Recommended actions:**
- Investigate stores with inventory availability below 85% (the dataset mean is 88.3%)
- Prioritise stock replenishment for high-footfall stores where out-of-stock has the highest opportunity cost

### Priority 4 — Improve Customer Rating
A 1-star improvement in customer rating is associated with £13,389 more in monthly sales. This is one of the most cost-effective levers if improvements can be driven through training and process rather than capital investment.

**Recommended actions:**
- Audit low-rated stores (rating < 3.5) and identify root causes
- Invest in staff training programmes focused on customer experience
- Track rating as a KPI alongside sales in monthly reviews

### Priority 5 — Use Marketing Spend Strategically
The marketing coefficient drops from £2.13 (in simple regression) to £1.17 (in multiple regression) once footfall and other factors are controlled. This suggests that some of the apparent marketing effect in SLR was actually driven by store size and footfall correlations.

**Recommended actions:**
- Marketing spend still shows a positive return (£1.17 per £1 spent) but is not the primary lever
- Focus marketing investment on low-footfall stores to drive visitor numbers rather than applying spend uniformly
- Measure marketing effectiveness by footfall uplift, not just sales uplift

---

## 3. Which Variables Should NOT Be Over-Interpreted?

### avg_discount_pct (p = 0.15 — Not Significant)
Discount percentage did not show a statistically significant relationship with sales in the multiple regression. This does NOT mean discounting has no effect — it means that within this dataset, the discount levels used did not systematically predict higher or lower sales once other factors were controlled.

**Do not** cut discounting based on this finding alone. A dedicated discount experiment (A/B test) would give cleaner evidence.

### region_North (p = 0.44 — Not Significant)
North region stores perform statistically similarly to East stores. No special treatment needed for North vs East from a sales driver perspective.

### store_Mall (p = 0.22 — Not Significant)
Mall stores perform comparably to Airport stores in this model. The Mall premium is not statistically distinguishable from Airport performance.

---

## 4. Business Actions Recommended

| Action | Based On | Expected Impact |
|--------|----------|----------------|
| Invest in footfall-driving initiatives across all stores | footfall coefficient (+£27.89/visitor) | High — largest individual driver |
| Prioritise Airport and Mall locations for new store openings | store type dummies | Avoid £22K–£42K monthly penalty of weaker types |
| Set inventory availability target ≥ 95% for all stores | inventory coefficient (+£3,112/1%) | Medium — consistent gains |
| Launch customer rating improvement programme | rating coefficient (+£13,389/star) | Medium — high ROI if driven by training |
| Shift marketing spend to low-footfall stores | marketing coefficient (+£1.17/£1) | Moderate — ensure marginal spend drives footfall |
| Investigate West region high-variance stores | residual analysis | Identify and fix under-performers (−£94K to −£166K residuals) |
| Study over-performing stores (STR-1028, STR-1030) for best practices | positive residuals | Replicate hidden success factors |

---

## 5. Why Regression Shows Association, Not Causation

This is a critical point for leadership to understand before making investment decisions.

Regression tells us: *"These variables move together with sales."* It does NOT tell us: *"If we change this variable, sales will definitely change by this amount."*

**Examples of why causation is uncertain:**

1. **Footfall and staff count**: Busy stores naturally hire more staff AND attract more customers. If we hired more staff at a quiet store, sales might not increase by £3,188 per hire — the model just observed that busy stores tend to have both.

2. **Customer rating**: High-rating stores may have better locations, better products, and better staff all at once. Improving just the rating score without addressing underlying service quality may not generate £13,389.

3. **Marketing spend**: Larger stores get larger marketing budgets from head office. The correlation partly reflects store size, not just marketing effectiveness.

**What to do instead of assuming causation:**
- Run controlled experiments (A/B tests) for each lever before large-scale investment
- Use the regression findings to *prioritise* where to run experiments, not as proof of what will work

---

## 6. Risks and Limitations

1. **Short time window**: Only 4 months of data (Jan–Apr 2025). Seasonal patterns are not fully captured — summer, back-to-school, and Christmas periods are missing.

2. **Missing variables**: The model cannot capture local competition intensity, nearby demographics, store age, refurbishment status, or manager quality — all of which likely affect sales.

3. **Multicollinearity**: Footfall and staff count are correlated (busier stores need more staff). Their individual coefficients should be interpreted carefully.

4. **No causal mechanism**: As explained above — association is not causation. Use findings as hypotheses, not confirmed levers.

5. **14 records with missing data**: 6 missing competitor_distance_km and 8 missing customer_rating values were imputed with median values. This introduces minor estimation error.

6. **R² = 0.8380**: Strong, but 16.2% of sales variation is unexplained. The model is a useful guide, not a perfect forecast tool.

---

## 7. Final Summary

The analysis clearly identifies **footfall, inventory availability, customer rating, and store type** as the most actionable drivers of monthly sales in this retail chain. Leadership should focus resources on driving more visitors into stores, ensuring products are in stock when customers arrive, and maintaining high service quality — particularly in Residential stores which significantly underperform Airport equivalents.

Marketing spend shows a positive but moderate return and should be targeted strategically at low-footfall locations rather than applied uniformly. Discounting strategy requires a dedicated experiment before any conclusions can be drawn from regression alone.
