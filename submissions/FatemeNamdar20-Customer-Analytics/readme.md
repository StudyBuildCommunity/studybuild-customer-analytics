# Email Campaign Effectiveness and Customer Value

An analysis of a randomized email marketing experiment using Kevin Hillstrom's *MineThatData* dataset.

The goal is to evaluate whether email campaigns increase website visits, purchases, and revenue, compare the performance of two campaign types, and explore which customer segments appear more responsive.

## Key Results

- **Experiment design:** 64,000 customers were randomly assigned to one of three groups: Men's Email, Women's Email, or No Email (control). Outcomes were measured over the following two weeks.
- **Higher visit rates:** The visit rate increased from 10.62% in the control group to 15.14% for Women's Email and 18.28% for Men's Email.
- **Higher conversion rates:** Conversion increased from 0.57% in the control group to 0.88% for Women's Email and 1.25% for Men's Email.
- **Statistical significance:** Both email groups had significantly higher conversion rates than the control group based on two-proportion z-tests (α = 0.05).
- **Revenue impact:** Revenue per customer increased from $0.65 in the control group to $1.08 for Women's Email and $1.42 for Men's Email.
- **Purchase behavior:** The increase in revenue per customer was mainly associated with more customers making purchases, rather than substantially higher spending per buyer. Average spend per buyer ranged from approximately $114 to $122.
- **Customer funnel:** Most of the observed improvement occurred at the website visit stage. The visit-to-purchase rate changed less than the overall visit rate.
- **Exploratory customer analysis:** The Men's Email campaign showed a larger revenue lift among high-value customers. However, subgroup findings are descriptive and require further statistical validation.

> The Men's Email campaign had the strongest observed performance across the main metrics. However, whether either campaign is profitable depends on campaign costs and profit margins, which are not provided in the dataset.

## Project Status

The exploratory analysis, campaign comparisons, funnel analysis, conversion tests, and preliminary revenue analysis have been completed.

The following areas are still in progress:

- **Section 12 – Statistical vs. Business Significance:** Further evaluation of the economic impact, including cost and profit-margin sensitivity analysis.
- **Section 14 – Customer Targeting:** Further investigation of customer-level campaign effects and targeting recommendations.

## Business Problem

A retailer conducted an email marketing experiment to understand the effectiveness of two promotional campaigns.

Customers were assigned to one of three groups:

- Men's Email: Received an email promoting men's merchandise.
- Women's Email: Received an email promoting women's merchandise.
- No Email: Received no promotional email and served as the control group.

The analysis addresses two main questions:

1. Do email campaigns increase website visits, purchases, and revenue? Which campaign performs better?
2. Do campaign effects vary across customer segments, and which customer characteristics may help identify responsive customers?

## Dataset

The dataset comes from Kevin Hillstrom's *MineThatData E-Mail Analytics and Data Mining Challenge* (2008).

It contains 64,000 customer records and 12 columns.

### Feature Description

| Column | Description |
|---|---|
| `recency` | Months since the customer's last purchase (1–12) |
| `history` | Total amount spent during the previous year |
| `history_segment` | Historical spending category |
| `mens` | 1 if the customer purchased men's merchandise during the previous year |
| `womens` | 1 if the customer purchased women's merchandise during the previous year |
| `zip_code` | Customer's area category: Urban, Surburban, or Rural |
| `newbie` | 1 if the customer was new within the previous 12 months |
| `channel` | Previous purchasing channel: Phone, Web, or Multichannel |
| `segment` | Assigned experimental group |
| `visit` | Whether the customer visited the website during the two weeks after the campaign |
| `conversion` | Whether the customer made a purchase during the following two weeks |
| `spend` | Amount spent during the following two weeks |

### Data Quality Notes

- No missing values were found.
- There are 6,562 exact duplicate rows. Since the dataset does not contain a customer ID and identical feature values may belong to different customers, these rows were retained.
- The three experimental groups have nearly equal sizes:
  - Men's Email: 21,307 customers
  - Women's Email: 21,387 customers
  - No Email: 21,306 customers
- Pre-campaign characteristics were broadly similar across the three groups, supporting the consistency of the random assignment.
- All customers had made at least one purchase during the previous year. Therefore, the findings describe existing active customers rather than the general population.
- Purchases were relatively rare: 14.7% of customers visited the website, while approximately 0.9% made a purchase.
- `spend` is zero for approximately 99.1% of customers.

## Methodology

The analysis follows these steps:

1. **Data Understanding and Quality Assessment:** Examining data types, missing values, duplicates, distributions, and descriptive statistics.
2. **Customer Value Analysis:** Segmenting customers into Low, Medium, and High value groups using historical spending (`history`).
3. **Customer Behavior Analysis:** Exploring relationships between customer characteristics and campaign outcomes, including recency, customer type, purchasing channel, and geographic area.
4. **Funnel Analysis:** Examining the customer journey from assignment to website visits and purchases.
5. **Campaign Performance Analysis:** Comparing visit rates, conversion rates, total revenue, and revenue per customer across the three groups.
6. **A/B Testing:** Applying two-proportion z-tests to compare the conversion rates of each email group against the control group.
7. **Revenue Analysis:** Evaluating revenue per customer, average spend per buyer, and incremental revenue relative to the control group.
8. **Customer Targeting (In Progress):** Exploring whether campaign effectiveness varies across different customer segments.

## Results

### 1. Campaign Funnel

| Group | Customers | Visitors | Buyers | Visit Rate | Conversion Rate | Visit-to-Purchase Rate |
|---|---:|---:|---:|---:|---:|---:|
| No Email | 21,306 | 2,262 | 122 | 10.62% | 0.57% | 5.39% |
| Women's Email | 21,387 | 3,238 | 189 | 15.14% | 0.88% | 5.84% |
| Men's Email | 21,307 | 3,894 | 267 | 18.28% | 1.25% | 6.86% |

The email campaigns were associated with higher visit and purchase rates.

The visit-to-purchase rate is calculated only among customers who visited the website. It is therefore a conditional descriptive metric rather than a direct estimate of the overall causal effect of the campaign.

### 2. A/B Testing: Conversion Rate

Two-proportion z-tests were used to compare each email group with the control group.

- Null hypothesis (H0): The two groups have equal conversion rates.
- Alternative hypothesis (H1): The two groups have different conversion rates.
- Significance level: α = 0.05.
- Test type: Two-sided.

| Comparison | Conversion Rate | Difference | Z-statistic | P-value | Result |
|---|---|---:|---:|---:|---|
| Men's vs. No Email | 1.25% vs. 0.57% | +0.68 pp | 7.385 | < 0.001 | Significant |
| Women's vs. No Email | 0.88% vs. 0.57% | +0.31 pp | 3.780 | 0.00016 | Significant |

Both email campaigns showed statistically significant increases in conversion compared with the control group.

Because customers were randomly assigned, the results support a causal interpretation of the average campaign effects, subject to the assumptions of the experiment and the analysis.

A direct statistical comparison between Men's and Women's Email is still needed.

### 3. Revenue Analysis

| Group | Total Revenue | Revenue per Customer | Average Spend per Buyer | Median Spend per Buyer |
|---|---:|---:|---:|---:|
| No Email | $13,908 | $0.65 | $114.0 | $88.4 |
| Women's Email | $23,038 | $1.08 | $121.9 | $94.7 |
| Men's Email | $30,312 | $1.42 | $113.5 | $67.0 |

Revenue per customer was calculated using the spending of all customers, including those who made no purchase.

Compared with the control group, the estimated additional revenue over the two-week period was approximately:

- **Men's Email:** $16,400
- **Women's Email:** $9,100

These estimates are based on the difference in revenue per customer multiplied by the corresponding email group's customer count.

The results suggest that higher revenue was mainly associated with increased purchasing activity rather than substantially higher average spending per buyer.

However, revenue does not represent profit. Campaign costs and profit margins must be considered before making a final business decision.

### 4. Customer Value Analysis

Customers were divided into three groups using historical spending:

- Low Value
- Medium Value
- High Value

The analysis compared revenue per customer in each value tier against the corresponding control group.

| Customer Tier | Control Revenue per Customer | Men's Email Revenue Lift | Women's Email Revenue Lift |
|---|---:|---:|---:|
| Low | $0.51 | +$0.56 | +$0.65 |
| Medium | $0.51 | +$0.71 | +$0.27 |
| High | $0.94 | +$1.05 | +$0.36 |

The Men's Email campaign showed a larger incremental revenue per customer among medium- and high-value customers, while Women's Email showed a larger lift in the low-value group.

These findings are exploratory. The number of buyers within individual segments is relatively small, so the differences should not be treated as statistically established.

### 5. Other Customer Characteristics

Additional exploratory analyses examined recency, customer type, purchasing channel, and geographic area.

- **Recency:** Visit rates generally decreased as the time since the previous purchase increased. Both email groups had higher visit rates than the control group across recency categories.
- **New vs. Existing Customers:** Existing customers were more active in the control group. Email campaigns also increased activity among new customers.
- **Purchasing Channel:** Multichannel customers had substantially higher historical spending and showed relatively high conversion and spending levels.
- **Geographic Area:** Rural customers had the highest observed conversion rates across the three experimental groups.

These observations describe customer behavior and campaign outcomes. They do not establish that the campaign effect differs significantly between these subgroups.

## Business Interpretation (Preliminary)

The observed results suggest that both email campaigns increased conversion and revenue per customer, with Men's Email showing the strongest overall performance.

A preliminary break-even analysis can help evaluate the economic value of the campaigns.

The additional revenue per customer compared with the control group was approximately:

- Men's Email: $0.77
- Women's Email: $0.42

Therefore, under a 100% contribution margin assumption, the campaign cost per customer would need to be below these amounts to break even on incremental revenue.

At a hypothetical 30% contribution margin, the corresponding break-even campaign costs would be approximately:

- Men's Email: $0.23 per customer
- Women's Email: $0.13 per customer

These are illustrative break-even thresholds, not estimates of actual profit. The dataset does not provide campaign costs or product margins.

## Limitations

- Outcomes were measured over only two weeks. Some purchases may have been brought forward rather than generated as additional long-term demand.
- The dataset contains revenue but does not include campaign costs or profit margins.
- The analysis covers customers who purchased during the previous year, not the general population.
- Purchases are rare, which makes subgroup-level estimates less stable.
- Multiple subgroup comparisons increase the risk of finding patterns by chance.
- The dataset does not contain a unique customer identifier. Exact duplicate rows were therefore retained.
- The direct comparison between Men's and Women's Email and the statistical validation of subgroup differences remain to be completed.

## Next Steps

- Complete the comparison between statistical and business significance.
- Evaluate the sensitivity of campaign profitability to different cost-per-email and profit-margin assumptions.
- Directly compare Men's and Women's Email performance.
- Apply an appropriate multiple-testing correction to the campaign comparisons.
- Evaluate revenue differences using Welch's t-test and/or bootstrap confidence intervals.
- Investigate whether campaign effects differ across customer value, customer type, and purchasing channel, for example using regression models with interaction terms.
- Complete the customer targeting analysis and develop evidence-based recommendations.
- Optionally explore uplift modeling to identify customers who are most likely to respond positively to an email campaign.

## How to Run

### Requirements

- Python 3.11
- Jupyter Notebook

### Installation

```bash
git clone <repository-url>
cd <repository-folder>
pip install pandas numpy matplotlib seaborn scipy statsmodels jupyter
```

### Dataset Setup

Place the dataset CSV file in the project root directory:

`Kevin_Hillstrom_MineThatData_E-MailAnalytics_DataMiningChallenge_2008.03.20.csv`

Open `Customer-Analytics.ipynb` in Jupyter Notebook and run the cells.

## Project Structure

```text
.
├── Customer-Analytics.ipynb
├── README.md
└── Kevin_Hillstrom_MineThatData_E-MailAnalytics_DataMiningChallenge_2008.03.20.csv
```

## Tech Stack

- **Programming Language:** Python 3.11
- **Data Manipulation:** Pandas, NumPy
- **Data Visualization:** Matplotlib, Seaborn
- **Statistical Analysis:** SciPy, Statsmodels
- **Development Environment:** Jupyter Notebook

## Acknowledgments

Dataset: Kevin Hillstrom, *MineThatData E-Mail Analytics and Data Mining Challenge* (2008).

## Author

**Fateme Namdarlo**
