## Executive Summary

The new onboarding and activation campaign (Treatment) achieved a statistically significant **+120.5% relative improvement** in paid conversion rate compared to the existing experience (Control). However, two critical guardrail metrics are severely breached: support ticket rates increased by +69.8% and revenue per converted user dropped by -52.7%.

**Recommendation: Do not launch broadly. Launch only for Free plan users while investigating guardrail breaches.**

---

## 1. Business Problem Statement

The company needs to decide whether to roll out the new onboarding campaign to all users. The decision impacts:
- **Product team** — whether to invest in scaling the new experience
- **Marketing team** — whether to expand campaign spend
- **Customer success team** — support capacity planning
- **Finance team** — revenue forecasting

The primary metric that must improve is **paid conversion rate**. Risks that must be monitored include support ticket volume, revenue quality per converted user, and refund rates. Evidence required: statistically significant conversion lift with no major guardrail breaches.

---

## 2. North Star Metric

**North Star: Paid Conversion Rate**

This is the single most direct measure of whether the campaign achieves its purpose — converting users to paid subscribers. It connects directly to revenue growth, customer lifetime value, and business sustainability.

**Why not other metrics?**
- Landing page visit rate and trial start rate are leading indicators, not outcomes
- ARPU can be influenced by plan mix — conversion rate is cleaner
- Engagement score is a health metric, not a conversion outcome

**Risk of blind optimisation:** If optimised without guardrails, the campaign could attract low-value converters, inflate support costs, and erode revenue quality — as seen in this experiment.

---

## 3. KPI Tree Summary

```
NORTH STAR: Paid Conversion Rate
│
├── DRIVER 1: Funnel Engagement
│   ├── Landing Page Visit Rate    (63.6% → 72.6% ✓)
│   ├── Trial Start Rate           (25.1% → 29.1% ✓)
│   └── Onboarding Completion Rate (15.6% → 21.3% ✓)
│
├── DRIVER 2: Revenue Quality
│   ├── Avg Revenue per User (ARPU)    ($51.75 → $53.88 ~)
│   ├── Revenue per Converted User     ($1,630 → $770 ✗)
│   └── Days to Convert               (8.9 → 6.4 days ✓)
│
└── DRIVER 3: User Experience
    ├── Engagement Score       (57.0 → 62.9 ✓)
    ├── Support Ticket Rate    (21.9% → 37.2% ✗ HIGH RISK)
    └── Refund Rate            (0.0% → 0.4% ~ watch)

GUARDRAIL METRICS:
  [G1] Refund Rate                       < 5% threshold     → 0.42% (OK)
  [G2] Support Ticket Rate               < 25% threshold    → 37.2% (BREACHED)
  [G3] Avg Revenue per Converted User    decline monitoring → -52.7% (BREACHED)
  [G4] Segment-level decline no region down                 → all regions up (OK)      
```

---

## 4. Experiment Result Summary

| Metric | Control | Treatment | Lift | Status |
|--------|---------|-----------|------|--------|
| Users | 685 | 707 | — | Balanced |
| Paid Conversion Rate | 3.21% | 7.07% | +120.5% | ✓ Significant |
| Onboarding Completion | 15.58% | 21.26% | +36.4% | ✓ Positive |
| Engagement Score | 57.03 | 62.93 | +10.3% | ✓ Positive |
| Days to Convert | 8.86 | 6.40 | -27.8% | ✓ Positive |
| ARPU | $51.75 | $53.88 | +4.1% | ~ Marginal |
| Rev per Converted User | $1,630 | $770 | -52.7% | ✗ Risk |
| Support Ticket Rate | 21.93% | 37.20% | +69.8% | ✗ High Risk |
| Refund Rate | 0.00% | 0.42% | New | ~ Watch |

---

## 5. Hypothesis Test Interpretation

- **Test:** One-tailed Z-test for difference in proportions (Treatment > Control)
- **Z-score:** 3.2640
- **P-value:** 0.000549
- **Alpha:** 0.05
- **Decision:** REJECT H₀ — Treatment conversion rate is statistically significantly higher

The result is robust. A confirming Chi-Square test returned p=0.001672, also significant. The conversion improvement is not due to random chance.

---

## 6. Guardrail Analysis

### Support Ticket Rate — HIGH RISK
The Treatment group generated support tickets at 37.2% vs 21.9% for Control — a 69.8% increase. This breaches the acceptable threshold of 25%. At scale, this would create unsustainable support costs and signals that the new onboarding experience is causing confusion. Investigation needed: are certain onboarding steps unclear, are users experiencing bugs, or is the campaign attracting less technically-capable users?

### Revenue per Converted User — HIGH RISK
Despite more conversions, each converted user generates significantly less revenue ($770 vs $1,630). Total Avg Revenue per User (ARPU) improved only marginally (+$2.28), meaning the extra conversions are mostly low-value. Possible causes: the campaign is driving users toward lower-tier plans, or the campaign audience skews toward price-sensitive segments. This must be resolved before scaling.

### Refund Rate — MONITOR
Refund rate moved from 0% to 0.42% in Treatment. While small, the control had zero refunds. This should be tracked if the campaign is partially launched.

### Days to Convert — POSITIVE
Users convert 2.46 days faster under Treatment (6.4 vs 8.9 days). This is a healthy signal — the campaign is accelerating decision-making without creating regret (though the refund rate warrants continued monitoring).

---

## 7. Segment-Level Insights

**By Region:**
- Treatment outperforms Control in all 4 regions (North, South, East, West)
- North shows the highest lift: +5.44pp
- East shows the lowest lift: +3.87pp — still positive

**By Device Type:**
- Mobile shows strong lift: +4.77pp (vs 2.57% Control)
- Tablet shows strong relative lift: +5.35pp
- Desktop already had a higher base; lift is more moderate (+2.04pp)

**By Plan Type:**
- Free plan users show the largest relative lift: +6.19pp (3.05% → 9.24%)
- Premium plan users show solid lift: +3.50pp
- Basic plan users show marginal lift: +0.24pp — weakest response

**Insight:** The campaign is most effective for **Free plan users** and is consistently positive across all regions. Free plan users may be the ideal target segment for a partial launch.

---

## 8. Final Recommendation

### Decision: Launch only for Free plan users; do not broad launch

**Rationale:**
1. Conversion lift is statistically significant and practically meaningful (+120.5%)
2. However, the support ticket rate breach (+69.8%) makes a full launch operationally risky
3. Revenue per converted user drop (-52.7%) means the conversion lift is not translating to proportional revenue
4. Free plan users show the strongest conversion lift and represent the lowest-risk segment to target

**Recommended actions:**
1. Partially launch the campaign for **Free plan users only** — this is where lift is strongest
2. Task the product team with investigating why support tickets increased (UX audit of new onboarding flow)
3. Task revenue/pricing team with investigating why converted user revenue dropped (plan mix analysis)
4. Re-run the experiment after addressing the above issues before full launch
5. Add support ticket rate and revenue per converted user as blocking guardrails for any future launch decision

---

## 9. Risks and Limitations

- **Support cost risk:** At 37.2% ticket rate, scaling Treatment to all users would significantly increase support costs
- **Revenue quality risk:** Low revenue per conversion could hurt LTV metrics and investor metrics
- **Experiment duration unknown:** Seasonal effects not controlled for
- **8 duplicate user_ids removed:** Minor data quality issue; does not materially affect results
- **18 missing device_type and 24 missing traffic_source records:** Minor; segment analysis still valid
- **No long-term data:** 30-day revenue window; churn and LTV effects not yet visible

---

## 10. Next Steps

| Action | Owner | Timeline |
|--------|-------|----------|
| Partial launch to Free plan users | Product + Engineering | 2 weeks |
| UX audit of new onboarding steps | Product Design | 2 weeks |
| Revenue & plan-mix analysis for Treatment converters | Finance + Analytics | 1 week |
| Re-run experiment with revised campaign | Product + Marketing | 4-6 weeks |
| Define guardrail thresholds as hard launch gates | Analytics + Leadership | 1 week |
