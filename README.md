
# Minimum Sample Size Calculator

A lightweight sample size estimation tool for binomial metrics, supporting both longitudinal monitoring and A/B testing.

The tool also supports **weighted multi-page metrics (LDBOM)** and can compute either:

* **Required sample size for a target precision**
* **Detectable precision given existing sample size**

Built with **pure HTML/JS** — no dependencies.

---

# Features

* Supports **two statistical scenarios**

  * Longitudinal monitoring (paired comparison across periods)
  * A/B testing (independent two-sample comparison)

* Two calculation modes

  * **Precision → Sample Size**
  * **Sample Size → Precision**

* **Weighted multi-page metrics** (LDBOM model)

* Built-in **inverse normal distribution function**

* **Google Analytics tracking** for usage monitoring

* **No backend required** (static HTML tool)

---

# Scenarios

## Longitudinal Monitoring (Paired Samples)

Used when measuring the **same population across time periods**.

Examples:

* Monthly satisfaction rate monitoring
* Quarterly NPS tracking
* Detecting periodic fluctuations in key metrics

---

## A/B Testing (Independent Samples)

Used when comparing **two independent groups**.

Examples:

* New vs. old product experiments
* Strategy effectiveness testing
* Feature rollout evaluation

---

# Calculation Modes

| Mode                    | Input                | Output               |
| ----------------------- | -------------------- | -------------------- |
| Precision → Sample Size | Target MDE           | Required sample size |
| Sample Size → Precision | Existing sample size | Detectable MDE       |

---

# Key Parameters

| Parameter     | Description                                      | Default |
| ------------- | ------------------------------------------------ | ------- |
| `p`           | Expected proportion (e.g. 0.7 satisfaction rate) | —       |
| `δ (MDE)`     | Minimum Detectable Effect                        | —       |
| `α`           | Significance level                               | 0.2     |
| `power (1-β)` | Statistical power                                | 0.6     |

Recommended settings:

| Use Case            | α    | Power |
| ------------------- | ---- | ----- |
| Routine monitoring  | 0.2  | 0.6   |
| Important decisions | 0.05 | 0.8   |

---

# Core Formulas

### Z-score

```
Z = Zα/2 + Zβ
  = NORMSINV(1 − α/2) + NORMSINV(power)
```

Example (α=0.2, power=0.6)

```
Z = 1.282 + 0.253 = 1.535
```

---

### Longitudinal Monitoring

```
SE = √(p(1-p)/n)

MDE = Z × SE

n = Z² × p(1-p) / δ²
```

---

### A/B Testing

```
SE = √(pA(1-pA)/nA + pB(1-pB)/nB)

MDE = Z × SE
```

If **nA is fixed**, required **nB**:

```
VarA = pA(1-pA)
VarB = pB(1-pB)

nB = VarB / [(δ/Z)² − VarA/nA]
```

---

# Weighted Page Metrics (LDBOM)

Supports **five page types** for weighted aggregation.

| Code | Page    | Description                       |
| ---- | ------- | --------------------------------- |
| L    | List    | Search results page               |
| D    | Detail  | Product detail page               |
| B    | Booking | Reservation / checkout page       |
| O    | Order   | Order confirmation page           |
| M    | Message | Post-booking confirmation message |

Weighted standard error:

**Longitudinal**

```
SE = √(Σ wi² × pi(1-pi)/ni)
```

**A/B Test**

```
SE = √(Σ wi² × [pAi(1-pAi)/nAi + pBi(1-pBi)/nBi])
```

Weight rules:

* Weights should **sum to 1**
* Page-level MDE

```
δ_page = δ_total / w
```

---

# Confidence Intervals

| CI Level | Formula    |
| -------- | ---------- |
| 90%      | 1.645 × SE |
| 95%      | 1.960 × SE |
| 99%      | 2.576 × SE |

---

# Usage

## Mode 1 — Precision → Sample Size

1. Select scenario
2. Enter parameters (`p`, `δ`, `α`, `power`)
3. (Optional) Configure page weights
4. Click **Calculate Sample Size**

Output:

* Required total sample size
* Page-level sample requirements

---

## Mode 2 — Sample Size → Precision

1. Select scenario
2. Enter parameters (`α`, `power`)
3. Input page metrics (`p`, `n`, `weight`)
4. Click **Calculate Precision**

Output:

* Weighted MDE
* Confidence intervals
* Page-level MDE

---

# Tech Stack

* **HTML**
* **CSS**
* **Vanilla JavaScript**

Math utilities:

* Rational approximation for **inverse normal distribution**

Minimum enforced sample size:

```
n ≥ 200
```


---

# Version History

| Version | Date     | Notes                                 |
| ------- | -------- | ------------------------------------- |
| v3.0    | Mar 2026 | Added GA tracking, fixed A/B nB logic |
| v2.0    | Feb 2026 | Added A/B testing and LDBOM support   |
| v1.0    | Feb 2026 | Initial release                       |

---

# License

URS Data Science Team © 2026

It would make the repo look **10× more professional**.

