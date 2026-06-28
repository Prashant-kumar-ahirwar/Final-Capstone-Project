# Chart Selection Justification
**Dashboard:** Retail Executive Dashboard
**Analyst:** Business Analyst

---

## Chart 1 — Monthly Sales Trend: Line Chart with Dual Axis

| Attribute | Detail |
|:---|:---|
| Business question | How are sales and margin changing over time? |
| Chart type | Line chart (primary) + Line chart on dual axis (secondary) |
| Why appropriate | Lines show continuous change over time — ideal for trend data |
| Fields used | X: Order Date (Month), Y1: SUM(Sales), Y2: Profit Margin % |
| Color principle | Blue for Sales (primary/positive), Orange for Margin (secondary/alert) |
| Design principle applied | Dual axis avoids two separate charts while preserving scale clarity |
| Mistake avoided | Did NOT use a bar chart — bars imply discrete comparison, not trend |

---

## Chart 2 — Regional Sales: Horizontal Bar Chart

| Attribute | Detail |
|:---|:---|
| Business question | Which region generates the most sales and best margin? |
| Chart type | Horizontal bar chart |
| Why appropriate | Compares 4 discrete categories; horizontal layout gives space for labels |
| Fields used | Y: Region, X: SUM(Sales), Color: Region, Label: Profit Margin % |
| Color principle | Consistent regional color scheme (South=Blue, North=Teal, etc.) throughout |
| Design principle applied | Sorted descending by Sales so reader immediately sees rank |
| Mistake avoided | Did NOT use a pie chart — bars make magnitude comparison far clearer |

---

## Chart 3 — Sub-Category Profit: Horizontal Bar Chart

| Attribute | Detail |
|:---|:---|
| Business question | Which sub-categories are profitable and which are destroying value? |
| Chart type | Horizontal bar chart with diverging axis |
| Why appropriate | Shows both positive (profit) and negative (loss) values clearly |
| Fields used | Y: Sub-Category, X: SUM(Profit), Color: Category |
| Color principle | Color encodes parent category for immediate grouping |
| Design principle applied | Zero reference line distinguishes profitable vs loss-making |
| Mistake avoided | Did NOT hide negative bars — transparency about losses is essential for leadership |

---

## Chart 4 — Discount vs Profit: Bar Chart (Ordered Bands)

| Attribute | Detail |
|:---|:---|
| Business question | What happens to average profit as discount levels increase? |
| Chart type | Bar chart with ordered discount bands on X axis |
| Why appropriate | Discrete bands on X axis, continuous profit on Y — bar is appropriate |
| Fields used | X: Discount Band (ordered), Y: AVG(Profit), Color: Gradient by band |
| Color principle | Green→Amber→Red gradient signals increasing risk as discount rises |
| Design principle applied | Bands ordered by increasing discount to show progressive impact |
| Mistake avoided | Did NOT use a scatter plot of raw discounts — too much noise to see the trend |

---

## Chart 5 — Shipping Performance: Grouped Bar + Line (Dual Axis)

| Attribute | Detail |
|:---|:---|
| Business question | Which shipping mode is fastest and has the lowest return rate? |
| Chart type | Bar chart (delivery days) + Line overlay (return %) |
| Why appropriate | Bars show magnitude of delivery time; line overlays return rate for correlation |
| Fields used | X: Ship Mode, Y1: AVG(Delivery Days), Y2: Return Rate % |
| Color principle | Speed gradient (green=fast, red=slow); red diamonds for return rate |
| Design principle applied | Sorted by delivery speed to make the speed-return relationship visible |
| Mistake avoided | Did NOT use a table — visual encoding is faster to interpret for executives |

---

## Chart 6 — Region × Category Heatmap: Color-Encoded Matrix

| Attribute | Detail |
|:---|:---|
| Business question | Which region-category combinations are most and least profitable? |
| Chart type | Heatmap (highlight table) |
| Why appropriate | Shows 4×3 matrix of values in minimal space; color encodes magnitude |
| Fields used | Rows: Region, Columns: Category, Color: SUM(Profit) |
| Color principle | Red-Yellow-Green diverging palette; green=profit, red=loss |
| Design principle applied | Value labels in cells allow precise reading; color gives pattern at a glance |
| Mistake avoided | Did NOT use 12 separate bar charts — heatmap shows the full picture in one view |

---

## Chart 7 — Discount vs Margin Scatter Plot (Sub-Category Level)

| Attribute | Detail |
|:---|:---|
| Business question | Is there a relationship between discounting and margin at sub-category level? |
| Chart type | Scatter plot with bubble size encoding |
| Why appropriate | Shows correlation between two continuous variables (discount %, margin %) |
| Fields used | X: AVG(Discount %), Y: AVG(Margin %), Size: SUM(Sales), Color: Category |
| Color principle | Color encodes category for grouping; size shows commercial importance |
| Design principle applied | Bubble size prevents equal weighting of minor sub-categories |
| Mistake avoided | Did NOT use a line chart — there is no natural order between sub-categories |

---

## Chart 8 — KPI Cards: Summary Metrics Row

| Attribute | Detail |
|:---|:---|
| Business question | What is the overall business health at a glance? |
| Chart type | KPI cards (text cards with background color) |
| Why appropriate | Executives need instant access to 3–5 headline numbers before diving deeper |
| Fields used | Total Sales, Total Profit, Profit Margin %, Return Rate, Avg AOV, etc. |
| Color principle | Each KPI card has a distinct color; cooler colors for financial, warmer for ops |
| Design principle applied | Placed at top of dashboard so leaders see the big picture first |
| Mistake avoided | Did NOT put 10+ KPIs — capped at 8 most relevant to avoid cognitive overload |

---

## General Design Principles Applied

1. **Consistent color system** — regional and category colors are identical across all views
2. **Hierarchy** — KPIs at top, strategic views in middle, tactical detail at bottom
3. **Minimal clutter** — removed gridlines, borders, and tick marks where not needed
4. **Data-ink ratio** — maximised; no decorative elements
5. **Readable fonts** — minimum 7.5pt for data labels; 10pt+ for titles
6. **Meaningful sorting** — all bar charts sorted by the relevant metric (not alphabetically)
7. **Zero-line reference** — always shown on diverging charts (profit, margin)
