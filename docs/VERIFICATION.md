# Verification — 10 October 2026

The published Power BI report was downloaded from GitHub and its SHA-256 matched the original supplied report:

`a26989b81fafa163861ffa4d88ca073c8eaa9ba89e90089a02d19d2f4eede98d`

## Checks passed

- ZIP integrity check: all archive entries passed their CRC checks.
- Parsed 79 JSON definitions, including the three report pages and 49 visual containers.
- Checked 37 distinct direct column/measure references against the embedded model schema; none were unresolved. This check does not evaluate every expression or alias-based reference.
- Compared every source column in the sales, products, customers and stores CSVs to the embedded tables, accounting for saved type and currency conversions.
- Recomputed financial figures independently from quantity and USD product prices/costs, using integer cents.
- Confirmed 62,884 sales lines, 26,326 distinct orders and 197,757 units; total revenue $55,755,479.59 and gross profit $32,662,688.38.
- Reconciled the README's annual comparisons, 2017 category findings, customer purchase frequencies, unit economics, Touch Screen Phones margin and Australia channel shares at their stated rounding.
- Checked README local file links, archive integrity, three page definitions, 33 saved DAX measure definitions and active sales relationships to product, customer, store and date tables.

## Verification limits

Power BI Desktop was unavailable in the macOS audit environment. No native DAX execution, interactive filter behavior, native refresh, custom-visual rendering or visual export was tested. The structural and numerical checks above must not be described as a complete Power BI Desktop runtime test.

The report includes saved local Windows source paths. For refresh, extract the repository's CSV archive and update Power Query source paths in Power BI Desktop. Exchange rates are included in the source archive; the financial measures use the supplied USD product prices and costs.

The data ends on 20 February 2021, so 2021 is incomplete. Gross profit excludes operating expenses. Proposed investigations are analytical recommendations, not measured commercial results.
