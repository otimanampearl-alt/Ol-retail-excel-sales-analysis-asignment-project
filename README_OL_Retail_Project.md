# Retail Sales Data Analysis — Excel & Power Query

## Project Overview

This project demonstrates an end-to-end retail sales data preparation and analysis workflow using **Microsoft Excel and Power Query**.

The workbook combines two source datasets:

- `Transactions (Raw)` — 2,503 transaction records
- `Online Orders` — 3,200 online order records


## Objective

The objective was to:

1. Combine transaction and online-order data using the existing Power Query workflow.
2. Standardize fields such as state, category, product identifiers, and sales identifiers.
3. Validate revenue calculations.
4. Identify data-quality issues before analysis.
5. Produce reliable KPIs and business insights.
6. Present the results in a decision-friendly Excel dashboard.

## Methodology

### 1. Source inspection

The supplied workbook contains:

- `Transactions (Raw)`
- `Online Orders`
- `category`
- `state`
- `channel`
- `dashboard`

The workbook also contains Power Query connections for the transaction, online-order, and append queries.

### 2. Power Query / append logic

The two main datasets were treated as the source tables for the combined analysis:

**2,503 Transactions (Raw) + 3,200 Online Orders = 5,703 records**

The resulting `Cleaned Data` sheet follows the same overall logic as the existing append workflow rather than replacing it with an unrelated analysis.

### 3. Data cleaning and standardization

The validated cleaning process included:

- Standardizing state names and removing inconsistent whitespace.
- Standardizing category values.
- Filling missing raw categories using the existing ProductName-to-Category relationship.
- Filling ProductID for online orders from the product mapping present in the transaction data.
- Standardizing SalesID/StaffID into a common analytical field where available.
- Calculating online revenue as `Quantity × UnitPrice`.
- Using the validated `Total Amount` field for raw transactions.
- Retaining original problem fields for auditability.
- Flagging missing dates and missing sales identifiers instead of inventing values.

### 4. Revenue validation

The raw transaction table contains both:

- `TotalAmount (problem)`
- `Total Amount`

A validation check showed that **1,687 raw records** have a mismatch between `TotalAmount (problem)` and `Quantity × UnitPrice`.

However, the existing `Total Amount` field agrees with `Quantity × UnitPrice` across all 2,503 raw transaction records. Therefore, `Total Amount` was used for validated revenue analysis while the problem field was retained for quality review.

## Key Findings

| KPI | Validated Result |
|---|---:|
| Total records | 5,703 |
| Unique Order IDs | 5,703 |
| Total revenue | ₦172,518,842 |
| Average order value | ~₦30,251 |
| Total quantity | 22,546 |
| Raw transaction revenue | ₦83,516,646 |
| Online order revenue | ₦89,002,196 |

### Category performance

**Groceries** is the largest revenue category at approximately **₦84.71 million**, followed by:

- Electronics — ~₦35.66 million
- Fashion — ~₦34.63 million
- Baby Care — ~₦7.23 million
- Household — ~₦5.84 million
- Personal Care — ~₦4.45 million

### Monthly performance

Revenue by month was:

- April 2026 — ~₦46.53 million
- May 2026 — ~₦48.02 million
- June 2026 — ~₦40.97 million
- July 2026 — ~₦29.40 million

May was the strongest month in the supplied data.

## Business Insights

### 1. Groceries are the main revenue driver

Groceries contribute the largest share of revenue. Inventory availability and demand monitoring in this category can therefore have a significant effect on overall sales.

### 2. Online sales are commercially significant

The Online Orders dataset contributes approximately **₦89.00 million**, making digital sales an important part of the combined dataset.

### 3. Revenue performance varies by month

May records the strongest revenue, while July is substantially lower. The business should investigate whether this reflects seasonality, campaign timing, order volume, or incomplete reporting.

### 4. Data quality is a business issue

The analysis identified:

- 247 missing order dates.
- 481 online orders without SalesID.
- 1,687 raw records where the problem amount field disagrees with the calculated amount.
- Missing categories in the raw data that required product-based lookup.

These issues can affect reporting if they are not controlled upstream.

## Recommendations

1. **Standardize data entry rules** for dates, quantities, unit prices, states, product IDs, and categories.
2. **Use validated revenue fields** in reporting rather than the known problem amount field.
3. **Require SalesID/StaffID capture** for online and offline transactions where staff attribution is required.
4. **Resolve missing order dates** before relying heavily on daily or monthly trend analysis.
5. **Monitor grocery inventory closely** because groceries are the largest revenue category.
6. **Create automated data-quality checks** within the Power Query workflow so missing values and calculation mismatches are detected during refresh.
7. **Maintain an audit layer** where original/problem fields remain available for review rather than being silently overwritten.

## Tools Used

- Microsoft Excel
- Power Query
- PivotTables / Pivot-based analysis
- Excel charts and dashboarding
- Data cleaning and validation
- GitHub / Markdown

## Conclusion

This project demonstrates how Excel and Power Query can be used to transform raw retail data into a structured analytical workflow.

The key learning was that **cleaning the data is part of the analysis**. Before building KPIs or dashboards, calculation fields, missing values, identifiers, categories, and other quality issues need to be validated.




---

### Portfolio note

This project is presented as an Excel + Power Query data-cleaning and business-analysis project. The focus is on demonstrating the workflow: source inspection → Power Query append → cleaning/standardization → validation → analysis → dashboard → business recommendations.
