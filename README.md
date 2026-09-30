# Global Electronics | Sales & Profitability Analytics

A three-page Power BI report exploring sales performance, product profitability, customer purchasing patterns, and channel mix for a fictitious global electronics retailer.

**Tools:** Power BI Desktop, Power Query, DAX, and relational data modeling.  
**Scope:** 62,884 sales line items, January 2016 to February 2021.  
**Author:** [Aman](https://github.com/AmanZayn7)

## Dashboard Previews

### Executive Overview

![Executive Overview](Executive-Overview.png)

### Product Economics

![Product Economics](Product-%20Economics.png)

### Customer & Channels

![Customer & Channels](Customer-Channels.png)

## Business Questions

| Page | Purpose | Key visuals |
| --- | --- | --- |
| Executive Overview | Assess performance and identify categories driving revenue changes. | KPI comparisons, monthly trends, channel mix, contribution waterfall, and category matrix. |
| Product Economics | Evaluate unit economics, margin quality, and profit concentration. | Cost/profit breakdown, profitability scatter, decomposition tree, and prior-year dumbbell comparison. |
| Customer & Channels | Understand purchase frequency and geographic differences in channel mix. | Online-share trend, country map, channel comparison, and purchase-frequency funnel. |

## Key Findings

- **2020 revenue decline was primarily volume-driven:** Revenue fell 49.1%, from $18.26M to $9.29M. Orders fell from 9,083 to 4,635, while average order value stayed near $2,000. The priority is investigating reduced purchasing activity.
- **Growth concealed category weakness:** In 2017, total revenue grew 6.8%. Computers contributed approximately $0.73M in additional revenue, while TV & Video revenue declined 35.3%.
- **Repeat purchasing was limited:** In 2017, 88.3% of purchasing customers placed exactly one order; 11.7% placed at least two. This highlights an audience for further repeat-purchase analysis.
- **Revenue scale alone does not establish margin quality:** The product page identifies products with meaningful revenue but below-portfolio gross margins for pricing and cost review.

## Technical Approach

- Organized sales analysis around `factSales`, supported by customer, product, store, and calendar tables.
- Used Power Query for data preparation and DAX for KPIs, prior-year comparisons, unit economics, and customer measures.
- Counted distinct order numbers and purchasing customers rather than treating sales line items as complete orders.
- Added filter-responsive narratives to highlight revenue contributors, products to review, customer loyalty, and geographic channel differences.
- Applied consistent navigation, year slicers, tooltips, conditional formatting, and supporting metrics within KPI cards.

## Data & Interpretation

**Source:** [Global Electronics Retailer - Maven Analytics](https://mavenanalytics.io/data-playground/global-electronics-retailer). Monetary measures use USD-based product prices and costs.

- **2021 is incomplete:** Records end on February 20, 2021. Compare matched periods rather than interpreting it as a completed year.
- **Gross profit is not net profit:** It excludes operating expenses not supplied in the dataset.
- **Repeat purchasing is period-specific:** It measures multiple orders within the selected filters, not lifetime retention. The funnel uses cumulative 1+, 2+, and 3+ order thresholds.
- **Findings are descriptive:** The dataset identifies patterns and contributions, but does not establish external causes for changes or prove business impact.

## Explore the Report

1. Download [the Power BI report](global%20electronics.pbix) and open it in Power BI Desktop.
2. Use the page navigation and year slicer to explore the measures and dynamic findings.
3. To refresh the data, extract [the dataset archive](Global%2BElectronics%2BRetailer.zip) and update local source paths in Power Query as needed.

The screenshots provide static previews. The `.pbix` contains the interactive report; custom visual rendering can vary across viewing and export environments.
