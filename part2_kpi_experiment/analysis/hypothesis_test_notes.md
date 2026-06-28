## 1. Business Context

The company launched a new onboarding and activation campaign for subscription users. Users were split into two groups:
- **Control:** Existing onboarding experience
- **Treatment:** New campaign experience

Leadership needs to know whether the treatment should be rolled out to all users.

---

## 2. Metric Being Tested

**Primary Metric: Paid Conversion Rate**  
(Number of users who converted to a paid plan / Total users in each group)

**Why this metric?**  
Paid conversion rate is the North Star metric for our experiment. It directly reflects the business objective — converting free/trial users into paying customers. It is the most direct signal of whether the new campaign achieves its intended purpose or not. All other metrics either support this metric (funnel metrics) or guard against unintended harm (guardrail metrics).

---

## 3. Hypotheses

### Null Hypothesis (H₀)
> The paid conversion rate in the Treatment group is **equal to** the paid conversion rate in the Control group.
>
> H₀: [ p_treatment = p_control ]

### Alternate Hypothesis (H₁)
> The paid conversion rate in the Treatment group is **greater than** the paid conversion rate in the Control group.
>
> H₁: [ p_treatment > p_control ]

---

## 4. Test Design

| Parameter | Value |
|-----------|-------|
| Test type | One-tailed Z-test for difference in proportions |
| Direction | Right-tailed (testing if Treatment > Control) |
| Significance level (alpha) | 0.05 (5%) |
| Test statistic | Z-score |
| Why one-tailed? | We are specifically testing if the treatment *improves* conversion, not just whether it differs |
| Why Z-test? | Large sample sizes (n_c=685, n_t=707), binary outcome (converted/not), proportions test |

---

## 5. Test Inputs

| Input | Value |
|-------|-------|
| Control group size (n_c) | 685 |
| Treatment group size (n_t) | 707 |
| Control conversions | 22 |
| Treatment conversions | 50 |
| Control conversion rate (p_c) | 3.2117% |
| Treatment conversion rate (p_t) | 7.0721% |
| Pooled proportion | 0.051975 |
| Standard error (SE) | 0.010523 |

---

## 6. Test Output

| Statistic | Value |
|-----------|-------|
| Z-score | 3.2640 |
| One-tailed p-value | 0.000549 |
| Critical value (alpha=0.05) | 1.645 |
| Chi-Square statistic | 9.8782 |
| Chi-Square p-value | 0.001672 |
| Degrees of freedom | 1 |

---

## 7. Decision Rule

- If p-value < 0.05 → **Reject H₀** (Treatment is significantly better)
- If p-value ≥ 0.05 → **Fail to reject H₀** (Not enough evidence)

**Result: p-value = 0.000549 < 0.05 → REJECT H₀**

---

## 8. Interpretation

The Z-score of 3.26 is well beyond the critical value of 1.645. The one-tailed p-value of 0.000549 is far below the 0.05 significance threshold. This means:

- There is **statistically significant evidence** that the Treatment group has a higher paid conversion rate than the Control group.
- The probability of observing a difference this large by chance alone (if the null were true) is less than 0.06%.
- The treatment produced a **+3.82 percentage point absolute lift**, representing a **+120.5% relative improvement** in conversion rate (from 3.21% to 7.07%).

---

## 9. Guardrail Metric Evaluation

Statistical significance alone is **not sufficient** for a launch decision. The following guardrail metrics were evaluated:

| Guardrail Metric | Control | Treatment | Change | Risk Level |
|------------------|---------|-----------|--------|------------|
| Support Ticket Rate | 21.93% | 37.20% | +15.27pp (+69.8%) | **HIGH RISK** |
| Revenue per Converted User | $1,630.10 | $770.41 | -$859.69 (-52.7%) | **HIGH RISK** |
| Refund Rate | 0.00% | 0.42% | +0.42pp | Moderate |
| Days to Convert | 8.86 days | 6.40 days | -2.46 days (-27.8%) | Positive |
| Engagement Score | 57.03 | 62.93 | +5.90 (+10.3%) | Positive |

### Critical Guardrail Breach: Support Ticket Rate
A 69.8% increase in support tickets is a major operational risk. This suggests the new onboarding experience may be confusing or creating friction that users need help resolving. At scale, this would significantly increase support costs and degrade customer experience.

### Critical Guardrail Breach: Revenue per Converted User
Although more users are converting, each converted user is generating significantly less revenue ($770 vs $1,630). This raises a serious concern: is the campaign attracting lower-value users, or offering discounts that undermine revenue quality? Total ARPU improved only marginally (+$2.13), meaning the conversion lift is not translating into proportional revenue gain.

---

## 10. Business Interpretation

The new campaign successfully increases paid conversion rate in a statistically significant manner. However, two major guardrail metrics are breached:

1. Support ticket rates are unsustainably high at 37.2%
2. Revenue per converted user has dropped by more than half

**Recommendation: Do not launch broadly at this time.**

The experiment should be paused, and the product/CX team should investigate:
- Why support tickets increased so dramatically
- Whether the pricing or plan structure of conversions has changed
- Whether the treatment works better for specific segments (Free plan users show particularly strong lift)

A revised campaign addressing the guardrail issues should be re-tested before full launch.

---

## 11. Assumptions and Limitations

- Users were assumed to be randomly and independently assigned to groups
- The deduplication (8 duplicate user_ids removed) may have slightly altered group sizes
- Chi-square test corroborates the Z-test result (p=0.001672)
- No multiple testing correction applied as only one primary metric was tested
- The experiment duration is not specified; seasonal effects cannot be ruled out
