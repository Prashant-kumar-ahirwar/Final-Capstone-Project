# Part 2 — KPI & Experiment Analysis

## Business Context

A subscription-based digital product company launched a new onboarding and activation campaign. Users were randomly split into two groups:

- **Control (685 users):** Existing onboarding experience
- **Treatment (707 users):** New campaign experience

Raw dataset contained 1,408 records. After removing 8 duplicate user_ids (keeping first occurrence), the final analysis used 1,392 records.

Leadership needs to decide whether to roll out the new campaign to all users. This project frames the business problem, defines success metrics, analyses the experiment results, evaluates guardrail metrics, and delivers a data-backed recommendation.

---

## Dataset Description

| Property | Detail |
|----------|--------|
| File | `campaign_experiment_data.xlsx` |
| Total Records (raw) | 1,408 |
| Records after dedup | 1,392 |
| Columns | 16 |
| Key fields | user_id, experiment_group, region, device_type, traffic_source, plan_type, funnel flags (binary), revenue_30d, support_tickets_30d, refund_requested, days_to_convert, engagement_score |

### Data Quality Issues Found
- 8 duplicate user_ids → removed, kept first occurrence
- 18 missing device_type values → excluded from device-level segment analysis
- 24 missing traffic_source values → excluded from traffic segment analysis
- 14 missing engagement_score values → excluded from engagement average calculation
- 1,336 null days_to_convert → expected (only 72 users converted; null = did not convert)
- Revenue outliers (max: $8,610) → retained as valid premium users

---

## North Star Metric

**Paid Conversion Rate** — the proportion of users in each group who converted to a paid subscription within 30 days.

This metric was chosen because:
- It directly measures the campaign's core objective
- It connects to revenue, LTV, and sustainable business growth
- All funnel metrics (landing page visits, trial starts, onboarding completions) lead into it
- It is measurable, unambiguous, and attributable to the experiment

Risk of blind optimisation: conversion rate can be inflated by targeting low-value or high-churn users, or by offering unsustainable discounts — as observed in this experiment.

---

## KPI Tree Summary

```
NORTH STAR: Paid Conversion Rate
├── DRIVER 1: Funnel Engagement
│   ├── Landing Page Visit Rate
│   ├── Trial Start Rate
│   └── Onboarding Completion Rate
├── DRIVER 2: Revenue Quality
│   ├── Avg Revenue per User (ARPU)
│   ├── Revenue per Converted User
│   └── Days to Convert
└── DRIVER 3: User Experience
    ├── Engagement Score
    ├── Support Ticket Rate
    └── Refund Rate

GUARDRAILS: Refund Rate | Support Ticket Rate | Rev/Converted User | Segment Decline
```

Full KPI tree image: `outputs/kpi_tree.png`

---

## Experiment Analysis Approach

1. Loaded and deduplicated the raw dataset (8 duplicate user_ids removed)
2. Checked group balance: Control=685, Treatment=707 (adequately balanced)
3. Validated all binary columns (all values 0 or 1, no anomalies)
4. Computed all 11 required metrics for Control and Treatment
5. Performed segment-level analysis across region, device type, traffic source, and plan type
   - 18 missing device_type values excluded from device segment analysis
   - 24 missing traffic_source values excluded from traffic segment analysis
6. Identified guardrail metric breaches

---

## Hypothesis Test Summary

| Parameter | Value |
|-----------|-------|
| Test | One-tailed Z-test (proportions) |
| H₀ | p_treatment = p_control |
| H₁ | p_treatment > p_control |
| Alpha | 0.05 |
| Z-score | 3.2640 |
| P-value | 0.000549 |
| Decision | REJECT H₀ |

The Treatment group shows a statistically significant improvement in paid conversion rate. The result is confirmed by Chi-Square test (p=0.001672).

---

## Guardrail Metrics Considered

| Guardrail | Control | Treatment | Status |
|-----------|---------|-----------|--------|
| Support Ticket Rate | 21.93% | 37.20% | BREACHED (threshold: 25%) |
| Revenue per Converted User | $1,630 | $770 | BREACHED (-52.7% drop) |
| Refund Rate | 0.00% | 0.42% | Watch (new occurrence) |
| Days to Convert | 8.86 days | 6.40 days | Positive |

---

## Final Recommendation

**Do not launch broadly. Launch only for Free plan users while investigating guardrail breaches.**

Key reasoning:
- Conversion lift is statistically significant (+120.5% relative)
- Support ticket rate increase is unsustainable at scale (+69.8%)
- Revenue per converted user has dropped significantly (-52.7%)
- Free plan users show the strongest lift with lowest risk profile

---

## Assumptions and Limitations

- Random assignment to groups assumed (not verified from raw data)
- 30-day revenue window only; long-term LTV effects unknown
- Seasonal or external effects not controlled
- No multiple testing correction needed (single primary metric tested)
- Duplicate user resolution (keep first) may have minor group size impact

---

## Screenshots Included

| File | Description |
|------|-------------|
| `screenshots/summary_metrics.png` | Control vs Treatment metric comparison table |
| `screenshots/hypothesis_test_output.png` | Z-test inputs, output, and distribution visualisation |
| `screenshots/kpi_tree_preview.png` | KPI tree diagram |
