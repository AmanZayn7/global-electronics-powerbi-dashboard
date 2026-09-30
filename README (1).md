# Global Electronics | Sales & Profitability Analytics

A three-page Power BI report connecting executive performance, product economics, and customer behavior for a fictitious global electronics retailer. The report combines performance monitoring with contribution analysis and dynamic findings to identify where further investigation would be useful.

**Tools:** Power BI Desktop, Power Query, DAX, and relational data modeling.  
**Scope:** 62,884 sales line items, January 2016 to February 2021.  
**Author:** [Aman](https://github.com/AmanZayn7)

[Download the report](global%20electronics.pbix) | [Source dataset](https://mavenanalytics.io/data-playground/global-electronics-retailer)

> Sales records end on February 20, 2021. The dataset contains all 12 months for 2016-2020, but 2021 is incomplete.

## Contents

- [Dashboard previews](#dashboard-previews)
- [Business questions](#business-questions)
- [Business insights and findings](#business-insights-and-findings)
- [Technical implementation](#technical-implementation)
- [Metric definitions and interpretation](#metric-definitions-and-interpretation)
- [Explore the report](#explore-the-report)

## Dashboard Previews

### Executive Overview

![Executive Overview](Executive-Overview.png)

<details>
<summary><strong>View Product Economics</strong></summary>

![Product Economics](Product-%20Economics.png)

</details>

<details>
<summary><strong>View Customer & Channels</strong></summary>

![Customer & Channels](Customer-Channels.png)

</details>

## Business Questions

| Page | Questions answered | Analytical approach |
| --- | --- | --- |
| **Executive Overview** | How are revenue, profit, and orders performing? Which categories explain the change? | KPI comparisons, monthly trends, channel mix, category waterfall, and a supporting matrix. |
| **Product Economics** | How much gross profit does each unit generate? Which products combine scale with margin quality? Where is profit concentrated? | Unit-economics breakdown, profitability scatter, profit decomposition, and a prior-year dumbbell comparison. |
| **Customer & Channels** | How frequently do customers purchase? How does online share vary over time and across countries? | Customer KPIs, online-share trend, customer geography, country-level channel mix, and purchase-frequency analysis. |

## Business Insights and Findings

The findings below refer to specific years and filter contexts. They demonstrate how the report supports investigation; proposed actions are recommendations for further analysis, not measured business outcomes.

### 1. The 2020 Revenue Decline Was Primarily Volume-Driven

Revenue fell **49.1%**, from **$18.26M in 2019 to $9.29M in 2020**. The number of distinct orders fell at almost the same rate, while average order value changed very little.

| Metric | 2019 | 2020 | Change |
| --- | ---: | ---: | ---: |
| Revenue | $18.26M | $9.29M | -49.1% |
| Distinct orders | 9,083 | 4,635 | Approximately -49.0% |
| Units sold | 68,440 | 34,463 | Approximately -49.6% |
| Average order value | $2,010.83 | $2,005.31 | Approximately -0.3% |

**Interpretation:** The business processed fewer orders and sold fewer units. Customers who did place orders spent nearly the same amount per transaction. This makes lower purchasing volume the main arithmetic explanation for the revenue decline.

**Where to investigate:** Break the order decline down by month, category, country, and channel. Distinguish fewer purchasing customers from fewer orders per customer before recommending an acquisition or repeat-purchase initiative.

**Boundary:** The dataset does not prove why demand fell. Explanations such as the pandemic, stock availability, or changes in marketing require additional evidence.

### 2. Positive Overall Growth Concealed Category Weakness

In **2017**, total revenue increased **6.8% to $7.42M**. Computers contributed approximately **$0.73M** in additional revenue, while TV & Video revenue fell **35.3% to approximately $0.82M**.

**Interpretation:** Growth was uneven. The gain in Computers offset weakness elsewhere, so the positive headline alone would have understated category-level risk. Absolute revenue contribution and percentage growth answer different questions: a large category can drive the result even when a smaller category has a higher growth rate.

**Where to investigate:** Use the revenue waterfall to identify the largest positive and negative contributions, then compare their revenue scale and margins in the matrix. Drill into the weaker categories to determine whether declines are concentrated in particular subcategories or brands.

### 3. Meaningful Revenue Does Not Automatically Indicate Strong Margin Quality

The **2017 Product to Review** narrative highlighted Touch Screen Phones: approximately **$309K in revenue at a 56.3% gross margin**, around **2.2 percentage points below the portfolio benchmark**.

The page also shows the overall unit economics for that selection:

| Metric | 2017 value |
| --- | ---: |
| Average selling price | $299.28 per unit |
| Cost per unit | $124.38 per unit |
| Gross profit per unit | $174.90 per unit |

**Interpretation:** Selling price alone does not describe profitability. The relationship between selling price and unit cost determines how much gross profit remains. A product below the portfolio margin may still be profitable and commercially important; it is a candidate for review rather than an automatic removal decision.

**Where to investigate:** Compare pricing, unit costs, brand mix, and product-level volume. Use the scatter plot to assess revenue scale alongside margin, and the decomposition tree to locate profit concentration. Any price or assortment change would need demand and competitive evidence beyond this dataset.

### 4. Purchasing Customers Were Concentrated in One-Order Buyers

In **2017**, the report identified **2,907 purchasing customers**. Of these, **2,567 (88.3%)** placed exactly one order, **340 (11.7%)** placed at least two, and **29 (1.0%)** placed at least three.

**Interpretation:** Most customers contributed through a single order in the selected year. This supports closer analysis of repeat-purchase behavior, but electronics can have long replacement cycles, so one order is not automatically evidence of dissatisfaction or churn.

**Where to investigate:** Compare repeat purchasing across categories, countries, and channels. Separate first-time buyers from established customers and consider category-specific purchase cycles before proposing follow-up campaigns or cross-selling.

**Boundary:** The purchase-frequency groups are cumulative. The 3+ group is contained within 2+, which is contained within 1+; these are not separate populations to add together.

### 5. Country-Level Channel Mix Revealed Differences Hidden by the Overall Share

In **2017**, online sales accounted for approximately **18.7% of total revenue**. Australia generated approximately **5.1% of revenue**, with an online share of **24.8%**, approximately **6.1 percentage points above the overall share**.

**Interpretation:** A country's revenue size and its channel mix are separate dimensions. A smaller revenue market can have a stronger online mix than the portfolio, while a larger market may remain predominantly store-based.

**Where to investigate:** Assess countries using both revenue scale and online share. Compare customer reach, revenue per customer, and repeat purchasing to understand whether a higher online share reflects a broader customer base or a concentrated group of buyers.

**Boundary:** A higher online share is a descriptive signal, not proof of greater channel profitability or unmet online demand.

## Technical Implementation

### 1. Power Query: Cleaning and Data Preparation

The preparation stage converted the source CSV tables into usable inputs for financial measures and date-based analysis.

| Preparation task | Implementation | Why it matters |
| --- | --- | --- |
| Currency-text cleaning | Removed currency symbols and thousands separators from product unit-price and unit-cost fields before converting them to decimal numbers. | Enables arithmetic on numeric values rather than formatted text. |
| Date normalization | Assigned date types to order dates, delivery dates, customer birthdays, store opening dates, and exchange-rate dates. | Supports consistent date interpretation and calendar-based analysis. |
| Query organization | Used fact/dimension naming to distinguish sales transactions from descriptive tables. | Makes table roles and measure dependencies easier to follow. |
| Multi-table preparation | Prepared sales, product, customer, store, and exchange-rate sources separately. | Preserves each table's grain and avoids conflating descriptive records with sales transactions. |

Blank source fields, such as missing delivery dates, should not be interpreted as zero-day delivery. Exchange rates are part of the source package; the report's monetary calculations use the supplied USD product prices and costs rather than claiming an exchange-rate conversion workflow.

### 2. Data Modeling and Calendar Design

The model centers on **`factSales`**, with active relationships to product, customer, store, and calendar tables. Customer, product, and store keys connect the corresponding attributes to sales analysis.

**Grain:** A row in `factSales` is an order line. An order containing multiple products can therefore appear on multiple rows. Distinct order counts are necessary for order KPIs and average order value.

**Calendar:** A dedicated `dimDate` was created using a DAX calendar construction with `CALENDAR` and `ADDCOLUMNS`, based on the sales date range. It provides the year and month context for slicers, monthly trends, and prior-year comparisons.

**Separation of concerns:** Source preparation handles types and source structure; model relationships support filtering; reusable measures own the business calculations. The same measures can therefore be used across KPI cards, charts, matrices, and narratives.

### 3. DAX: Reusable Measures and Advanced Analytical Logic

The measure layer combines financial calculations with customer-level evaluation and dynamic text. Its more involved work lies in evaluating customers individually, selecting relevant findings under filters, and comparing product performance with a broader benchmark.

#### Financial and Unit-Economics Measures

The report uses reusable revenue, cost, gross-profit, units, and order measures as inputs to derived KPIs. Unit economics are calculated from aggregate totals, so products with different sales volumes are weighted appropriately.

<details>
<summary><strong>View selected DAX examples</strong></summary>

```dax
Gross Profit per Unit =
DIVIDE([Gross Profit], [Total Units Sold])

Average Selling Price =
DIVIDE([Total Revenue], [Total Units Sold])

Average Order Value =
DIVIDE([Total Revenue], [Total Orders])
```

These ratios recalculate in the current filter context. They are not unweighted averages of product prices or averages of category-level ratios. `DIVIDE` provides defined behavior when the denominator is zero; without an alternative result, it returns a blank.

</details>

#### Customer-Level Segmentation and Context Transition

Repeat purchasing is calculated by evaluating distinct orders for each customer visible in the current filter context.

<details>
<summary><strong>View the repeat-customer measure and explanation</strong></summary>

```dax
Repeat Purchasing Customers =
COUNTROWS(
    FILTER(
        VALUES(factSales[CustomerKey]),
        CALCULATE(
            DISTINCTCOUNT(factSales[Order Number])
        ) >= 2
    )
)
```

- `VALUES` creates the distinct customer set in the current context.
- `FILTER` evaluates the order threshold for each customer.
- `CALCULATE` performs context transition so the distinct order count is evaluated for that customer.
- `COUNTROWS` returns the number of customers meeting the threshold.

This avoids counting several line items from the same order as several purchases. The result changes with the selected year and other filters, so it describes repeat purchasing within that context.

</details>

The customer measures extend this analysis to repeat purchase rate, revenue per purchasing customer, repeat buyer revenue share, and cumulative purchase-frequency thresholds.

#### Prior-Year Comparisons and Contribution Analysis

Revenue and gross-profit comparisons use prior-year measures to calculate both **absolute changes** and **percentage changes**.

- Absolute category revenue changes feed the waterfall, explaining how category gains and losses combine into the net change.
- Revenue YoY % gives a relative comparison in KPI cards and the matrix.
- Gross-profit current/prior-year measures feed the dumbbell chart.
- The calendar provides the date context for these comparisons; incomplete periods still require care when interpreting the results.

The distinction matters: ranking categories by percentage growth would not show which contributed the most dollars to the business-wide change.

#### Filter-Responsive Narrative Measures

The report uses DAX text measures to produce descriptive findings that update with the selected year rather than relying on fixed annotations.

| Narrative | Analytical logic communicated |
| --- | --- |
| **Key Findings** | Combines revenue level, YoY direction, and the category contributing most to the change. |
| **Where to Investigate** | Highlights a weaker category and provides a focused next step. |
| **Product to Review** | Presents a relevant product/subcategory's revenue, margin, and gap to the portfolio benchmark. |
| **Customer Loyalty** | Summarizes one-order buyers and customers meeting higher purchase-frequency thresholds. |
| **Geographic Channel Signal** | Compares a selected country's revenue share and online mix with the overall benchmark. |

These narratives combine entity selection, contextual metric evaluation, comparisons, and text presentation. They surface a useful interpretation alongside the visuals without claiming an external cause for the observed pattern.

### 4. Visual Design and Analytical Interaction

Visuals were chosen for different analytical tasks, not simply to increase the number of chart types.

| Visual | Purpose | Design consideration |
| --- | --- | --- |
| **Revenue line chart** | Compare current and prior-year monthly performance. | Both revenue series share a common scale to avoid misleading comparisons. |
| **Profit/margin combination chart** | Compare gross-profit dollars with the margin rate. | Separate units are identified because dollars and percentages have different meanings. |
| **Revenue waterfall** | Explain category contributions to the net change. | Gains and losses use distinct colors; values represent changes, not category revenue totals. |
| **Profitability bubble chart** | Evaluate revenue scale, margin, and gross-profit magnitude together. | X = revenue; Y = gross margin; bubble size = gross profit, with category grouping. |
| **Decomposition tree** | Explore gross profit through category, subcategory, and brand. | Supports interactive contribution exploration rather than a fixed hierarchy screenshot alone. |
| **Dumbbell chart** | Compare current and prior-year gross profit by category. | Connected endpoints emphasize the size and direction of the difference. |
| **Unit-economics stacked bar** | Show how selling price divides into cost and gross profit per unit. | Cost per unit plus gross profit per unit equals average selling price. |
| **Country map and channel bars** | Show geographic customer revenue and country-specific channel mix. | Country revenue magnitude and channel share are separate questions. |
| **Purchase-frequency funnel** | Compare the counts meeting increasing order thresholds. | Groups are cumulative, not stages of a sequential conversion process. |

The report also includes page navigation, year slicers, supporting KPI metrics, conditional formatting for positive/negative comparisons, and hover information. A consistent visual system keeps titles, spacing, colors, and containers aligned across the three pages.

### 5. Validation and Analytical Checks

The project included checks that address common sources of misleading results:

- Compared reported revenue and prior-year revenue with the displayed YoY calculation.
- Checked date coverage before interpreting the 2020 decline and partial 2021 results.
- Used distinct orders for order KPIs and customer purchase-frequency calculations.
- Corrected revenue-series axis scaling so their relative positions are interpretable.
- Standardized currencies, percentages, and large-number display units across visuals.
- Distinguished ratio calculations, cumulative customer groups, and gross profit from potentially misleading interpretations.

These are analytical consistency checks, not a claim of automated test coverage or a production deployment.

## Metric Definitions and Interpretation

| Metric | Definition |
| --- | --- |
| Total Revenue | Quantity multiplied by the supplied USD unit selling price, summed across sales lines. |
| Gross Profit | Revenue less product cost. Operating expenses are not included. |
| Gross Margin % | Gross profit divided by revenue. |
| Average Selling Price | Revenue divided by units sold. |
| Gross Profit per Unit | Gross profit divided by units sold. |
| Average Order Value | Revenue divided by distinct orders. |
| Repeat Purchase Rate | Customers with at least two distinct orders divided by purchasing customers in the selected context. |
| Repeat Buyer Revenue Share | Revenue from repeat purchasing customers divided by total revenue in the selected context. |
| Online Revenue Share % | Online revenue divided by total revenue; online transactions are identified using `StoreKey = 0`. |

**Additional interpretation notes:** The customer map reflects customer location rather than necessarily store location. Gross margin is not net margin. Narrative selections and values change with filters. Full-year and partial-year results need matched-period comparisons.

## Explore the Report

1. Download [the Power BI report](global%20electronics.pbix) and open it in Power BI Desktop.
2. Use page navigation and the year slicer to explore the measures and dynamic findings.
3. Hover over visuals for supporting metrics and expand the decomposition tree to investigate gross-profit contributions.
4. To refresh the data, extract [the dataset archive](Global%2BElectronics%2BRetailer.zip) and update local source paths in Power Query as needed.

Screenshots provide static previews. The `.pbix` contains the interactive report. Custom visual rendering may vary across viewing and export environments.

## Sources and Technical References

- [Global Electronics Retailer dataset - Maven Analytics](https://mavenanalytics.io/data-playground/global-electronics-retailer)
- [CALCULATE and context transition - Microsoft Learn](https://learn.microsoft.com/en-us/dax/calculate-function-dax)
- [DIVIDE behavior - Microsoft Learn](https://learn.microsoft.com/en-us/dax/divide-function-dax)

---

**Portfolio scope:** An independent analytics project demonstrating data preparation, measure design, business interpretation, and interactive reporting. Recommendations are proposed investigative actions, not claims of achieved commercial results.
