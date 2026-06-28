# Part 1 – Data Cleaning & Quality Report

## Problem Summary

A retail company exported order-level sales data from multiple internal systems. The raw dataset contained numerous quality issues including inconsistent text formatting, mixed date formats, duplicate records, missing values, invalid discounts, calculation mismatches, and order status inconsistencies. The goal of this project was to clean the dataset, apply business rules, validate data integrity, and produce summary reports for business review.

---

## Dataset Description

| Property | Detail |
|----------|--------|
| File | `raw_orders.xlsx` |
| Total Raw Records | 932 |
| Columns | 21 |
| Date Range | 2024 – 2025 |
| Key Fields | order_id, order/ship dates, customer info, product info, financials, order status |

The dataset covers orders across 4 regions (North, South, East, West), 3 product categories (Furniture, Technology, Office Supplies), and 4 customer segments (Consumer, Corporate, Small Business, Home Office).

---

## Tools Used

- **Python 3** – data cleaning and automation
- **pandas** – data manipulation, parsing, aggregation

---

## Cleaning Steps Performed

### Step 1 – Text Standardisation
All text fields (`customer_name`, `segment`, `region`, `state`, `city`, `category`, `sub_category`, `ship_mode`, `payment_status`, `order_status`) were cleaned by:
- Stripping leading and trailing spaces
- Collapsing multiple internal spaces into one
- Applying consistent Title Case
- Fixing known variant spellings (`Small  Business` → `Small Business`, `Standard  Class` → `Standard Class`)

### Step 2 – Date Parsing and Standardisation
The raw data contained three different date formats (`21 Jul 2024`, `08/31/2024`, `2024-05-24`, `28-11-2024`). A custom parser was written to handle all variations. All dates were standardised to `DD-MM-YYYY` format. A `shipping_delay_days` column was calculated as the difference between ship date and order date.

### Step 3 – Duplicate Removal and Flagging
- 20 exact duplicate rows were identified and removed
- 12 records shared duplicate `order_id` values with conflicting data — these were flagged in the `duplicate_flag` column and retained for review (first occurrence treated as canonical)

### Step 4 – Missing Value Handling
- `region` (25 nulls) → filled as `Unknown`
- `ship_mode` (21 nulls) → filled as `Unknown`
- `discount` (26 entries treated as missing: 18 true nulls + 8 text values like "70%"/"85%") → filled as `0` where other financial fields were valid

### Step 5 – Discount Validation
- 15 records had negative discounts → flagged as Invalid
- 7 records had discounts above 50% → flagged for review

### Step 6 – Calculated Columns Added
New columns added to `cleaned_orders.xlsx`: `cleaned_discount`, `calculated_sales`, `calculated_profit`, `profit_margin`, `shipping_delay_days`, `order_month`, `order_year`, `data_quality_flag`.

---

## Business Rules Applied

| Rule | Action |
|------|--------|
| Missing region | Filled as Unknown, flagged |
| Missing ship_mode | Filled as Unknown, flagged |
| Missing discount | Treated as 0 |
| Negative discount | Flagged as Invalid |
| Discount > 50% | Flagged for review |
| Cancelled orders | Excluded from pivot sales summaries |
| Failed payments | Excluded from pivot sales summaries |
| Refunded orders | Summarised separately in pivot sheet 5 |
| Ship date before order date | shipping_delay_days set to blank, flagged Invalid |

---

## Summary of Data Quality Issues Found

| Issue Type | Count |
|------------|-------|
| Exact duplicate rows removed | 20 |
| Conflicting duplicate order_ids flagged | 12 |
| Missing region values | 25 |
| Missing ship_mode values | 21 |
| Missing discount values | 26 (18 nulls + 8 unparseable text) |
| Negative discounts | 15 |
| Discounts above 50% | 7 |
| Ship date before order date | varies |

**Final cleaned dataset:** 912 records  
- ✅ Clean: 825 records  
- ⚠️ Warning: 51 records  
- ❌ Invalid: 36 records  

---

## Summary of Final Pivot Reports

| Sheet | Description |
|-------|-------------|
| 1. By Region | Total sales and profit by region, sorted by sales descending |
| 2. By Category | Sales and profit broken down by category and sub-category |
| 3. By Ship Mode | Order count and total sales per shipping mode, sorted by count |
| 4. By Segment | Average profit margin per customer segment, sorted descending |
| 5. Issues by Region | Count of cancelled and returned orders by region |
| 6. Monthly Trend | Month-by-month sales, profit, and order count (chronological) |

---

## Key Business Insights

1. **West region leads in total sales volume**, followed closely by South — both should be priority markets for inventory planning.
2. **Technology category** generates the highest average profit margins, making it strategically important despite smaller order volumes.
3. **Standard Class shipping** is the most frequently used mode, suggesting customers favour cost savings over speed.
4. **Corporate segment** shows a strong profit margin profile compared to Consumer and Small Business segments.
5. **Cancelled and returned orders are non-trivial** — regional managers should investigate patterns, especially in regions with high return rates.
6. **Monthly sales show seasonal peaks** — certain months consistently outperform others, which could inform promotional planning.

---

## Assumptions and Limitations

- Discount values are decimals (0.2 = 20%), not percentages
- Maximum valid discount threshold set at 50%
- First occurrence of conflicting `order_id` records was kept as canonical
- Ambiguous dates (e.g., `01/02/2024`) resolved by trying multiple format patterns in order
- No product master list was available to validate product or sub-category consistency
- Profit margin calculations may show extreme values where sales are very small

---

## Screenshots

| File | Description |
|------|-------------|
| `screenshots/raw_data_preview.png` | Raw dataset before any cleaning |
| `screenshots/cleaned_data_preview.png` | Cleaned dataset with calculated columns and quality flags |
| `screenshots/pivot_summary_1.png` | Total sales by region (bar chart) |
| `screenshots/pivot_summary_2.png` | Average profit margin by customer segment (bar chart) |
