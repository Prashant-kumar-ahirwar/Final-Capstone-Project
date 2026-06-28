# Cleaning Log – Raw Orders Dataset
**Analyst:** Capstone Project  
**Date:** June 2025  
**Tool:** Python 3 (pandas, openpyxl)

---

## 1. Issues Found in Raw Data

### Text Fields
- Inconsistent casing: e.g., `COMPLETED`, `completed`, `Completed ` all present in `order_status`
- Leading/trailing/extra spaces across `segment`, `region`, `ship_mode`, `payment_status`, `order_status`
- Variant spellings: `Small  Business` (double space), `Standard  Class` (double space)
- `ship_mode` contained `STANDARD CLASS`, `FIRST CLASS` in uppercase

### Date Fields
- Three mixed date formats used: `DD MMM YYYY` (e.g., `21 Jul 2024`), `MM/DD/YYYY`, `YYYY-MM-DD`, `DD-MM-YYYY`
- Several ship dates parsed as earlier than order dates (invalid shipping records)
- A small number of order dates and ship dates could not be parsed

### Duplicates
- **20 exact duplicate rows** found (all fields identical)
- **12 additional records** share duplicate `order_id` values but contain conflicting data

### Missing Values
- `region`: 25 null values
- `ship_mode`: 21 null values
- `discount`: 26 entries treated as missing (18 true nulls + 8 text values like "70%"/"85%" that could not be parsed as decimals)

### Discount Issues
- **15 records** with negative discount (invalid)
- **7 records** with discount above 50% (flagged for review)

### Calculation Mismatches
- Several records where reported `sales` did not match `quantity × unit_price × (1 – discount)` by more than ₹1

---

## 2. Cleaning Actions Performed

### Text Cleaning
- Applied `.strip()` to remove leading/trailing spaces on all text columns
- Applied `.str.replace(r'\s+', ' ')` to collapse internal multiple spaces
- Applied `.str.title()` for consistent Title Case across all text fields
- Manually mapped `Small  Business` → `Small Business`, `Standard  Class` → `Standard Class`

### Date Cleaning
- Wrote a custom `parse_date()` function supporting 8 date format patterns
- Standardised all output dates to `DD-MM-YYYY` format
- Created `shipping_delay_days` = `ship_date – order_date` in days
- Records with ship date < order date: `shipping_delay_days` set to blank and flagged

### Duplicate Handling
- Removed all 20 exact duplicate rows silently (truly identical records)
- Kept first occurrence of conflicting duplicate `order_id` records
- Flagged all subsequent conflicting duplicates in `duplicate_flag` column (not removed)

### Missing Values
- `region` null → filled as `Unknown`, noted in quality flag
- `ship_mode` null → filled as `Unknown`, noted in quality flag
- `discount` null → filled as `0` (only where other sales fields were valid)

---

## 3. Business Rules Applied

| Rule | Action |
|------|--------|
| Missing region | Filled as `Unknown`, flagged in data_quality_report |
| Missing ship_mode | Filled as `Unknown`, flagged in data_quality_report |
| Missing discount | Treated as 0 if other sales fields valid |
| Negative discount | Flagged as `Negative discount - invalid` in `discount_flag` |
| Discount > 50% | Flagged as `Discount above 50% - review` in `discount_flag` |
| Cancelled orders | Excluded from pivot sales/profit summaries |
| Failed payments | Excluded from pivot sales/profit summaries |
| Refunded orders | Summarised separately in pivot sheet 5 |
| Ship date before order date | `shipping_delay_days` set to blank; flagged as Invalid |

---

## 4. Assumptions Made

1. Discount values are expressed as decimals (0.2 = 20%), not percentages.
2. Maximum allowed discount is 50% (0.5). Values above this are flagged but not removed.
3. For conflicting duplicate `order_id` records, the **first row in the raw file** is treated as the canonical record.
4. A sales mismatch tolerance of ₹1.00 is applied to account for rounding differences.
5. The formula for `calculated_sales` is: `Quantity × Unit Price × (1 – cleaned_discount)`.
6. The formula for `calculated_profit` is: `calculated_sales – cost`.
7. `Returned` orders with `Refunded` payment status are summarised separately and excluded from net completed sales.
8. Date formats were parsed using Indian business date conventions (DD-MM-YYYY as primary).

---

## 5. Records Removed

| Type | Count | Reason |
|------|-------|--------|
| Exact duplicate rows | 20 | All fields identical – no information loss |

---

## 6. Records Flagged (Not Removed)

| Flag Type | Count |
|-----------|-------|
| Duplicate order_id (conflicting) | 12 |
| Negative discount | 15 |
| Discount > 50% | 7 |
| Missing/invalid date issues | varies |
| Sales mismatch | varies |

All flagged records are visible in `cleaned_orders.xlsx` via the `data_quality_flag` column  
(`Clean` / `Warning` / `Invalid`) and the individual flag columns.

---

## 7. Limitations

- Date parsing relies on pattern matching; ambiguous dates like `01/02/2024` could be Jan 2 or Feb 1 – resolved by trying multiple formats in priority order.
- Conflicting duplicate records are flagged but not resolved – a business owner should review them.
- Profit margin calculation may produce very large values where `calculated_sales` is very small; these are retained but should be reviewed.
- No product master list was available to validate `product_name` or `sub_category` consistency.
- `order_id` uniqueness is assumed to be the primary business key; this assumption may not hold if the system allows split shipments.
