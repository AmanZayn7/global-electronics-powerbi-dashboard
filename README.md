# global-electronics-powerbi-dashboard
Power BI sales analytics dashboard for executive, product, and customer/channel insights.
Global Electronics | Sales & Profitability Analytics
A three-page report that connects executive sales performance with product economics and customer behavior. Built using a fictitious global electronics retailer's data, it helps users move from what changed to where to investigate next.
Scope: 62,884 sales line items, January 2016 to February 2021. Monetary measures use USD-based product prices and costs.
Coverage note: 2016-2020 contain all 12 months. Sales records end on February 20, 2021; 2021 must not be interpreted as a completed financial year.

Dashboard Preview
Executive Overview
 
Product Economics
 


Customer & Channels
 

Business Questions
Page	Questions answered	Analytical approach
Executive Overview	How are revenue, profit, and orders performing? Which categories explain the revenue change?	Prior-year comparisons, monthly trends, profit/margin combination chart, channel mix, category waterfall, and supporting matrix.
Product Economics	How much gross profit does each unit generate? Which products combine scale with strong margins? Where is profit concentrated?	Unit-cost/profit breakdown, revenue-margin bubble chart, category-to-subcategory-to-brand decomposition, and gross-profit dumbbell comparison.
Customer & Channels	How frequently do customers purchase? How does online share vary over time and across countries?	Customer KPIs, online-share trend, geographic revenue map, country-level channel mix, and purchase-frequency funnel.


Year slicers, page navigation, tooltips, and dynamic narrative measures make the report explorable rather than a collection of static charts. KPI supporting metrics provide context alongside the headline numbers.
Selected Findings
1. The 2020 decline was primarily a volume issue
Revenue fell from $18.26M in 2019 to $9.29M in 2020, a 49.1% decline. Distinct orders fell by approximately 49%, while average order value remained nearly unchanged.
| Metric | 2019 | 2020 |
| --- | ---: | ---: |
| Revenue | $18.26M | $9.29M |
| Orders | 9,083 | 4,635 |
| Average order value | $2,010.83 | $2,005.31 |

Implication: Investigate the reduction in purchasing activity before assuming lower transaction values caused the decline. This is an observed pattern, not proof of its external cause.
2. Overall growth can conceal category weakness
In 2017, revenue grew 6.8% to $7.42M. Computers contributed approximately $0.73M in additional revenue, while TV & Video declined 35.3% to approximately $0.82M.
Implication: Category-level contribution is essential: a positive business-wide headline does not mean every product category is improving.
3. Customer activity was concentrated in one-order buyers
In 2017, 2,567 of 2,907 purchasing customers (88.3%) placed exactly one order; 340 (11.7%) placed at least two. Only 29 placed at least three.
Implication: This identifies an audience for investigating repeat-purchase opportunities. It does not establish churn or measure customer lifetime retention.
4. Product scale and margin should be assessed together
The Product Economics page highlights products with meaningful revenue but gross margins below the portfolio benchmark. The scatter plot, unit-economics breakdown, and dynamic Product to Review narrative provide complementary views of these candidates.
Implication: Review pricing, unit costs, and product mix before prescribing a price increase. A below-average margin is a review signal, not automatically an unprofitable product.
Data & Analytical Design
The dataset is the Global Electronics Retailer sample available through Maven Analytics. It contains transactions, products, customers, stores, and exchange rates for a fictitious retailer.
The report centers on factSales, supported by customer, product, store, and calendar tables. The calendar supports year selection and prior-year analysis; product attributes support category, subcategory, and brand exploration.
Transaction grain matters: Each sales row represents an order line, not a complete order. Order KPIs therefore use distinct order numbers, and customer KPIs use distinct purchasing customers rather than counts of sales rows.
Power Query supports data preparation; DAX measures provide reusable calculations, comparison metrics, and filter-responsive narrative text. The report combines native visuals with custom map and dumbbell visuals.
Core Metric Definitions
Metric	Definition / interpretation
Total Revenue	Sum of quantity multiplied by USD unit selling price.
Gross Profit	Revenue less product cost; not net profit.
Gross Margin %	Gross profit divided by revenue.
Revenue YoY %	Revenue change relative to the prior-year comparison value.
Average Order Value	Revenue divided by distinct orders.
Average Selling Price	Revenue divided by units sold; quantity-weighted.
Gross Profit per Unit	Gross profit divided by units sold.
Purchasing Customers	Distinct customers with purchases in the current filter context.
Repeat Purchase Rate	Customers with at least two distinct orders divided by purchasing customers, within the selected period.
Repeat Buyer Revenue Share	Revenue from repeat purchasing customers divided by total revenue, within the selected period.
Online Revenue Share %	Online revenue divided by total revenue.


Interpretation & Limitations
- Partial-year comparisons: Use matched date ranges when evaluating 2021 against earlier years. A partial year is not comparable with a full year.
- Observed drivers, not causal proof: Category contribution explains the arithmetic of a change. The data does not establish causes such as COVID-19, stockouts, or marketing effectiveness.
- Margin is not net earnings: Product-cost-based gross profit excludes operating expenses and other costs not supplied in the dataset.
- Geography: The customer map represents customer location, not necessarily the location of the store that fulfilled an order.
- Purchase frequency: The funnel's 1+, 2+, and 3+ groups are cumulative thresholds, not mutually exclusive segments or a sequential conversion funnel.
- Dynamic summaries: Narrative values and highlighted categories respond to the selected filters. Screenshots show particular selections, not necessarily all-period totals.
- Custom visuals: Rendering and export support depend on the visual and environment. The screenshots preserve the map view, which did not render in the project's PDF export.
Explore the Report
1. Download (global electronics.pbix) and open it in Power BI Desktop.
2. Navigate between the three report pages and select a year to explore the KPI comparisons and dynamic findings.
3. Hover over visuals for supporting information; use the decomposition tree to explore gross-profit contributions.
4. To refresh from the source files, extract the dataset provided and update local file paths in Power Query as needed.
The screenshots above can be viewed without installing Power BI. They are static previews; the .pbix contains the interactive report.
Repository Contents
File	Purpose
global electronics.pbix	Interactive Power BI report.
Executive-Overview.png	Executive report preview.
Product- Economics.png	Product economics preview.
Customer-Channels.png	Customer and channels preview.
Global+Electronics+Retailer.zip	Source dataset archive.
README.md	Project context, findings, metric definitions, and usage notes.


Skills Demonstrated
Business-question framing; relational data modeling; Power Query preparation; DAX measures and time intelligence; weighted unit economics; customer segmentation; contribution analysis; conditional formatting; dynamic narratives; and consistent interactive report design.
Author: Aman
Project type: Independent analytics portfolio project using a fictitious retail dataset. Findings illustrate analytical reasoning; no real-world business impact is claimed.
