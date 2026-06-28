# Part 4 — Tableau Executive Dashboard & Data Storytelling

## Business Problem Summary
The retail leadership team needs an executive dashboard to monitor sales performance,
profitability, customer segments, category performance, shipping efficiency, discount
impact, and return patterns across 4 regions, 3 categories, and 3 customer segments.

## Dataset Description
| Property | Detail |
|:---|:---|
| File | `data/dashboard_sales_data.xlsx` |
| Records | 4,200 order lines |
| Date range | Jan 2024 – Dec 2025 |
| Regions | East, North, South, West |
| Categories | Furniture, Office Supplies, Technology |
| Sub-categories | 13 (Accessories, Art, Binders, Bookcases, Chairs, Copiers, Furnishings, Labels, Machines, Paper, Phones, Storage, Tables) |
| Segments | Consumer, Corporate, Home Office |
| Ship modes | First Class, Same Day, Second Class, Standard Class |
| Campaign channels | Email, Organic, Paid, Referral, Social |
| Missing values | customer_rating: 32 null, campaign_channel: 24 null |

## Tableau Workbook Description
**File:** `tableau/executive_dashboard.twbx`

The workbook contains the following sheets:
1. **Sales Trend** — Monthly line chart with profit margin dual axis
2. **Regional Performance** — Bar chart + heatmap by region
3. **Category Profitability** — Sub-category profit bars + margin analysis
4. **Customer Segments** — Grouped comparison of 3 segments
5. **Shipping Performance** — Delivery days + return rate by ship mode
6. **Discount vs Profit** — Discount band bar chart with margin line
7. **Return Analysis** — Return rate by region, category, segment
8. **Campaign Channel** — Sales and profit by acquisition channel
9. **Executive Dashboard** — Combined view with KPI cards and all 8+ views

## Calculated Fields Created
| Field | Tableau Formula | Purpose |
|:---|:---|:---|
| Profit Margin | `[Profit] / [Sales]` | Profitability KPI |
| Cost | `[Sales] - [Profit]` | Cost of goods baseline |
| Average Order Value | `SUM([Sales]) / COUNTD([Order ID])` | Revenue efficiency |
| Return Rate | `SUM([Return Flag]) / COUNT([Order ID])` | Operational risk KPI |
| Shipping Delay Bucket | IF/ELSEIF on [Delivery Days] | Categorise delivery speed |
| Discount Band | IF/ELSEIF on [Discount] | Group discounts meaningfully |
| Profitable Order | IF [Profit] > 0 | Flag profitable vs loss orders |
| Year-Month | `DATETRUNC('month', [Order Date])` | Time series grouping |

## Dashboard Components
- 8 KPI summary cards (Sales, Profit, Margin, Orders, AOV, Return Rate, Rating, Delivery)
- 10 chart views (line, bar, scatter, heatmap, stacked bar, bubble)
- 3 interactive filters: Region, Category, Customer Segment
- 4 additional filters: Date Range, Ship Mode, Discount Band, Campaign Channel
- 1 action filter: clicking region/category cross-filters all other views

## Key Business Insights
1. Technology drives 84.2% of profit at 18.2% margin
2. South region leads in sales and margin; East underperforms
3. Tables sub-category is consistently loss-making (5.7% margin)
4. Discounts >30% produce average LOSSES of ₹1,601/order
5. Home Office segment has the highest margin (15.5%)
6. Slow delivery (6+d) correlates with 4.8% return rate vs 4.3% for Express
7. Referral channel has highest profit per order
8. Q4 seasonal peaks require inventory buffer planning

## Dashboard Story Summary
The business is growing profitably, but margin is under threat from aggressive discounting
and loss-making products in Furniture. Technology and Home Office are the strategic growth
levers. Delivery speed improvements can reduce return rate and cost. See full story in
`outputs/dashboard_story.md`.

## Assumptions and Limitations
- Relationships shown are associative, not causal
- Missing rating/channel data excluded from relevant analyses
- State-level geographic views available but not the primary focus
- Seasonal patterns inferred from 2 years of data — more history would improve reliability

## Screenshots Included
| File | Shows |
|:---|:---|
| `screenshots/full_dashboard.png` | Complete executive dashboard with KPIs and all views |
| `screenshots/sales_trend_view.png` | Monthly sales trend, margin, quarterly and category breakdown |
| `screenshots/regional_performance_view.png` | Regional sales, margin, returns and heatmap |
| `screenshots/category_profitability_view.png` | Sub-category profit, margin, discount scatter |
| `screenshots/filter_interaction_view.png` | Dashboard under 4 different filter states |

> **Note on Tableau file:** The `.twbx` packaged workbook at `tableau/executive_dashboard.twbx`
> contains the full interactive dashboard. Open in Tableau Desktop 2023.1+ to explore filters
> and drill-down interactions.
