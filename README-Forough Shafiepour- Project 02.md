# Customer Analytics & A/B Testing

**StudyBuild — Project 02** · Author: Forough Shafiepour

An end-to-end customer analytics project on the Hillstrom Email Marketing dataset. It covers customer behavior, segmentation, funnel and campaign performance, A/B testing, incremental revenue, targeting, ROI and final business recommendations.

> **Headline result:** Both email campaigns increased conversion with statistical significance versus the No E-Mail control. Mens E-Mail was clearly stronger (conversion 1.25% vs 0.88% vs 0.57%) and, under the assumed economics, generated far more estimated incremental profit ($2,790 vs $584). Complex targeting models did not beat random selection.

## Contents

1. [Business Problem](#1-business-problem)
2. [Dataset](#2-dataset)
3. [Data Cleaning](#3-data-cleaning)
4. [Analysis Questions](#4-analysis-questions)
5. [Customer Segments](#5-customer-segments)
6. [Campaign Analysis](#6-campaign-analysis)
7. [A/B Testing](#7-ab-testing)
8. [Revenue, Targeting and ROI](#8-revenue-targeting-and-roi)
9. [Key Insights](#9-key-insights)
10. [Business Recommendations](#10-business-recommendations)
11. [Limitations](#11-limitations)
12. [How to Run](#12-how-to-run)

## 1. Business Problem

An online retailer ran an email experiment with three randomly assigned groups:

- **Mens E-Mail** — campaign promoting men's products
- **Womens E-Mail** — campaign promoting women's products
- **No E-Mail** — control group that received no campaign

The main business question is: **how can the company choose better customers for future campaigns, and did the current campaign actually increase purchasing?**

Sub-questions:

- Who are the most valuable customers, and how do new and existing customers differ?
- Which characteristics are associated with higher engagement and spending?
- Do the campaigns increase visits, conversion and revenue, and which one performs better?
- Can segmentation or targeting improve results?
- Are the campaigns profitable?

## 2. Dataset

| Property | Description |
|---|---|
| Dataset | Hillstrom Email Marketing (MineThatData E-Mail Analytics Challenge) |
| Records | 64,000 customers |
| Original columns | 12 |
| Campaign groups | Mens E-Mail (21,307), Womens E-Mail (21,387), No E-Mail (21,306) |
| Overall conversion | 578 buyers (0.90%) |

| Variable | Description |
|---|---|
| `recency` | Months since the customer's most recent purchase (1–12) |
| `history_segment` | Historical spending category |
| `history` | Historical customer spending ($) |
| `mens`, `womens` | Previous purchase of men's / women's products (not customer gender) |
| `zip_code` | Urban, Suburban or Rural |
| `newbie` | New (1) or existing (0) customer |
| `channel` | Web, Phone or Multichannel |
| `segment` | Email campaign assignment |
| `visit` | Visited the website after the campaign |
| `conversion` | Purchased after the campaign |
| `spend` | Spending after the campaign |

`visit`, `conversion` and `spend` are post-campaign outcomes, not customer characteristics.

## 3. Data Cleaning

| Check | Result | Action |
|---|---|---|
| Missing values | None | No imputation needed |
| Duplicate rows | 6,562 extra rows in 1,072 duplicate groups (7,634 rows involved) | Retained (see below) |
| Invalid values | No negative values; binary columns contain only 0/1; recency within 1–12 | None needed |
| Data types | Appropriate for analysis | None needed |
| Outliers (IQR) | `history`: 3,593 values (5.61%); `spend`: 578 values (0.90%) | Retained (see below) |
| Category labels | The ZIP label `Surburban` is misspelled in the source | Kept unchanged to match the source file; read it as "Suburban" |

**Duplicates.** The dataset has no unique customer ID, so identical rows may be repeated records *or* different customers with the same attributes. The 6,562 extra rows are about 10% of the data. Removing them could remove real customers and weaken the A/B test, so they were retained. Treat all counts as row-based rather than confirmed unique people.

**Outliers.** High `history` and `spend` values are plausible genuine behavior and carry business value, so they were retained. Because about 99% of customers have `spend = 0`, the IQR rule flags every positive spend value; this is a property of the data, not evidence of errors. Spend is therefore very right-skewed, and revenue estimates are less stable than conversion estimates.

## 4. Analysis Questions

| Question | Analysis |
|---|---|
| Q1 | Data quality |
| Q2 | Customer overview |
| Q3 | Customer value segmentation |
| Q4 | Recency analysis |
| Q5 | New vs existing customers |
| Q6 | Channel analysis |
| Q7 | Geographic analysis |
| Q8 | Customer funnel |
| Q9 | Campaign performance |
| Q10 | A/B test: Mens E-Mail vs No E-Mail |
| Q11 | A/B test: Womens E-Mail vs No E-Mail |
| Q12 | Statistical vs business significance |
| Q13 | Revenue analysis |
| Q14 | Customer targeting across segments |
| Q15 | Personalization by previous purchases |
| Q16 | 10,000-email targeting rule and uplift models |
| Q17 | Campaign ROI |
| Q18 | Final business recommendations |

Q1–Q13 and Q18 are the core requirements; Q14–Q17 are the advanced section.

## 5. Customer Segments

Customers were split by the medians of `history` ($158.11) and `recency` (6 months). These are relative thresholds, not absolute definitions of value.

| Segment | Customers | Share | Conversion | Revenue / customer |
|---|---:|---:|---:|---:|
| High Value / Recent | 20,686 | 32.3% | 1.30% | $1.40 |
| High Value / Inactive | 11,313 | 17.7% | 0.86% | $1.04 |
| Low Value / Recent | 15,899 | 24.8% | 0.77% | $0.98 |
| Low Value / Inactive | 16,102 | 25.2% | 0.57% | $0.69 |

Other customer-base findings:

- **Recency:** customers who purchased within 6 months have a 38% higher visit rate and 55% higher conversion rate than less recent customers.
- **New vs existing:** the base is split almost evenly (50.2% new). Existing customers visit more (17.3% vs 12.1%) and convert slightly more (1.01% vs 0.80%).
- **Channel:** Multichannel customers are only 12% of the base but the most valuable (average history $521, conversion 1.26%, $1.40 revenue per customer). Web has the highest total revenue.
- **Region:** Rural customers have the highest visit (18.8%) and conversion (1.12%) rates, but differences between regions are small.

## 6. Campaign Analysis

| Metric | Mens E-Mail | Womens E-Mail | No E-Mail |
|---|---:|---:|---:|
| Customers | 21,307 | 21,387 | 21,306 |
| Website visitors | 3,894 | 3,238 | 2,262 |
| Visit rate | 18.28% | 15.14% | 10.62% |
| Conversions | 267 | 189 | 122 |
| Conversion rate | 1.253% | 0.884% | 0.573% |
| Visit-to-purchase rate | 6.86% | 5.84% | 5.39% |
| Average spend per customer | $1.4226 | $1.0772 | $0.6528 |
| Total revenue | $30,311.69 | $23,038.11 | $13,908.33 |

**Funnel (Customers → Visit → Purchase).** The largest drop-off is between customer and visit: 89.4% of the control group never visits, compared with 81.7% (Mens) and 84.9% (Womens). Drop-off from visit to purchase stays above 93% in every group.

The raw numbers show Mens E-Mail performing best, but an observed difference alone does not prove a campaign effect. That is tested in the next section.

## 7. A/B Testing

Two-sided two-proportion z-tests were used. Customers were randomly assigned; History and Recency were balanced between Mens E-Mail and the control group (t-test p = 0.43 and 0.48).

| Comparison | Treatment | Control | Absolute lift | Relative lift | 95% CI (pp) | p-value |
|---|---:|---:|---:|---:|---|---|
| Mens vs No E-Mail | 1.253% | 0.573% | +0.681 pp | +118.8% | +0.50 to +0.86 | 1.5 × 10⁻¹³ |
| Womens vs No E-Mail | 0.884% | 0.573% | +0.311 pp | +54.3% | +0.15 to +0.48 | 0.000157 (Holm: 0.000314) |
| Mens vs Womens | 1.253% | 0.884% | +0.370 pp | — | — | 0.000205 (Holm: 0.000314) |

**Conclusion for the Marketing Manager.** Both emails increased the share of customers who buy, and the difference between them is also real. Mens E-Mail more than doubled the conversion rate. This is very unlikely to be chance, and all three comparisons stay significant after Holm adjustment for multiple tests.

**Statistical vs business significance (Q12).** A significant result means an effect exists, not that the campaign is worth running. The effect sizes are small in absolute terms (under one percentage point), so value was judged using revenue and ROI.

## 8. Revenue, Targeting and ROI

### Revenue (Q13)

| Metric | Mens E-Mail | Womens E-Mail | No E-Mail |
|---|---:|---:|---:|
| Revenue per customer | $1.42 | $1.08 | $0.65 |
| Average spend per converting customer | $113.53 | $121.89 | $114.00 |
| Incremental revenue per customer | $0.77 | $0.42 | — |
| Estimated total incremental revenue | $16,402.71 | $9,076.90 | — |

The campaigns raised revenue mainly by getting *more* customers to buy, not by making buyers spend more. Revenue estimates are less certain than conversion estimates because spend is highly skewed.

### Targeting and personalization (Q14–Q15)

- **Who responded (conversion lift vs control):** Mens E-Mail: +0.93 pp for customers with high purchase history, +1.02 pp for Multichannel, +0.74 pp for new customers, +0.73 pp for inactive customers. Womens E-Mail: +0.53 pp for new customers, +0.37 pp for inactive customers. After Holm adjustment, some of these subgroup differences remained significant (for example Mens E-Mail among new, high-history and Multichannel customers).
- **Personalization:** For Mens E-Mail, previous purchase of men's products did **not** significantly change the campaign effect (interaction p = 0.78). For Womens E-Mail it **did** (interaction p = 0.031): the email lifted conversion by +0.51 pp among customers who had bought women's products, but only +0.06 pp among those who had not.

### Targeting 10,000 emails and uplift models (Q16)

- **Uplift models (T-Learner, S-Learner):** For Mens E-Mail, customers picked by the models had *lower* lift than the overall validation lift. For Womens E-Mail the S-Learner was slightly better (0.38 vs 0.33), but evidence is weak.
- **Recency rule (target the most recent customers, scaled to a 10,000-email budget):** it did not beat random selection; about 59% of random selections performed as well or better, and bootstrap intervals include zero.
- **Budget split scenario:** among the scenarios tried, 4,000 Mens + 6,000 Womens emails had the highest estimated incremental profit ($3,071). Because this was the best of several scenarios, treat it as optimistic.

### ROI (Q17)

Assumptions: cost per email $0.10, profit margin 30% of incremental revenue.

| Metric | Mens E-Mail | Womens E-Mail |
|---|---:|---:|
| Emails sent | 21,307 | 21,387 |
| Campaign cost | $2,130.70 | $2,138.70 |
| Incremental revenue | $16,402.71 | $9,076.90 |
| Incremental profit | **$2,790.11** | **$584.37** |
| Break-even cost per email | $0.2309 | $0.1273 |

Both campaigns are profitable under these assumptions, but Womens E-Mail has a thin margin: its break-even cost ($0.127) is only slightly above the assumed cost ($0.10).

## 9. Key Insights

1. **Both campaigns work.** Mens E-Mail raised conversion from 0.57% to 1.25% (+119%) and Womens E-Mail to 0.88% (+54%); Mens is significantly better than Womens.
2. **The biggest drop-off is getting customers to visit.** Email moved visit rate from 10.6% to 18.3% (Mens) and 15.1% (Womens).
3. **High Value / Recent customers are the most valuable** ($1.40 revenue per customer vs $0.69 for Low Value / Inactive). Recent buyers and Multichannel customers respond best.
4. **Personalization matters for Womens E-Mail.** It works mainly for customers with previous purchases of women's products.
5. **Complex targeting did not pay off.** Uplift models and the Recency rule did not reliably beat random selection, so a simple broad send to engaged customers is a reasonable default for now.

## 10. Business Recommendations

1. **Prioritize Mens E-Mail in the next campaign.** It has the highest lift, revenue and profit, and about 2.3× headroom over the assumed cost per email. Keep monitoring before large budget expansion.
2. **Redesign and personalize Womens E-Mail, then re-test.** Send a women's-products version to customers who previously bought women's products, and test a different offer for those who did not.
3. **Prioritize High Value / Recent and Multichannel customers,** and design a separate re-activation test for High Value / Inactive customers.
4. **Keep a randomized control group in every campaign.** Without it, incremental impact cannot be measured.
5. **Judge campaigns by incremental profit, not conversion alone,** and recalculate with real email costs and margins.
6. **Do not adopt a complex targeting model yet.** Re-evaluate uplift models with more data and an external validation period.

## 11. Limitations

- **No unique customer ID:** results are row-based; duplicate-looking rows and overlap between campaign populations cannot be verified.
- **Rare outcome:** about 99% of customers did not buy, so revenue and subgroup estimates are noisy.
- **Skewed spend and retained outliers:** a few large purchases can influence average spend and revenue estimates.
- **Multiple comparisons:** subgroup analyses involve many tests; treat them as hypotheses for future experiments.
- **Uplift and targeting results:** models did not consistently beat random selection, and some scenarios were chosen using the same test data, so their estimated performance may be optimistic.
- **Economic assumptions:** ROI assumes $0.10 per email and a 30% margin; actual profitability may differ.
- **Single, historical campaign:** results come from one dataset and period; long-term effects such as email fatigue were not studied.

The results are evidence for further experimentation, not guaranteed future outcomes.

## 12. How to Run

**Requirements:** Python 3 with Jupyter. Libraries used: pandas, numpy, matplotlib, seaborn, scipy, statsmodels, scikit-learn, openpyxl, pyarrow.

```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels scikit-learn openpyxl pyarrow jupyter
```

**Repository structure**

```text
Project02-Customer-Analytics/
├── data/
│   └── Kevin_Hillstrom_MineThatData_E-MailAnalytics_DataMiningChallenge_2008.03.20.csv
├── notebook/
│   └── customer_analysis.ipynb
├── figures/                      # all key charts (PNG)
│   ├── customer_overview.png
│   ├── customer_segments.png
│   ├── recency_analysis.png
│   ├── new_vs_existing.png
│   ├── channel_analysis.png
│   ├── geographic_analysis.png
│   ├── campaign_funnel.png
│   ├── campaign_performance.png
│   ├── ab_test_mens_vs_no_email.png
│   ├── ab_test_womens_vs_no_email.png
│   ├── revenue_analysis.png
│   ├── targeting_lift_*.png      # customer type, purchase history, recency, channel, geography
│   └── campaign_incremental_profit.png
├── README.md
└── executive_summary.pdf
```

**Steps**

1. Download the repository and place the dataset in `data/`.
2. Open `notebook/customer_analysis.ipynb` in Jupyter.
3. In the first cell, set `DATA_PATH` to your local file, for example `"../data/Kevin_Hillstrom_MineThatData_E-MailAnalytics_DataMiningChallenge_2008.03.20.csv"`.
4. Run the cells in order. Some later cells reload an intermediate dataset (`df`) saved as a parquet file by earlier cells, so run from the top.
5. Charts are saved to `figures/`; the advanced analysis also exports an Excel workbook with model comparisons, subgroup results and budget scenarios.

> Some cells still contain local file paths from the original development environment (for example a `G:\` drive path). Update them before running on another computer.

---

**Focus:** Customer Analytics · A/B Testing · Segmentation · Campaign ROI · Uplift Modeling
**Tools:** Python · pandas · NumPy · Matplotlib · Seaborn · SciPy · Statsmodels · scikit-learn · Jupyter
