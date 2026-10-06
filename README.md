# DataCo Smart Supply Chain | Power BI Portfolio

An executive Power BI report for connecting commercial performance with delivery operations. Built to help a COO identify where revenue is concentrated, where order value is weakening, and which delivery risks deserve attention.

**Role:** Data Analyst (portfolio project) · **Audience:** COO · **Tools:** Power BI, DAX, data analysis

> **At a glance:** 180,519 order-item records · 65,752 distinct orders · 4 report pages · Dataset period: Jan 2015–Jan 2018

## Business problem and objective

Commercial and operations performance are often reviewed separately. This report brings them into one decision flow: assess overall health, examine revenue and profit patterns, inspect delivery performance, then prioritize actions using business impact.

The goal is to give the COO a concise, filterable view of performance and a starting point for targeted follow-up. The report is analytical decision support; it does not establish operational causes on its own.

## Dataset and scope

The project uses the **DataCo Smart Supply Chain** dataset by Constante, Silva, and Pereira (2019), [Mendeley Data, version 5](https://data.mendeley.com/datasets/8gx2fvg2k6/5), DOI [10.17632/8gx2fvg2k6.5](https://doi.org/10.17632/8gx2fvg2k6.5). The source lists a [CC BY 4.0 license](https://creativecommons.org/licenses/by/4.0/); retain attribution and license details when sharing permitted materials.

The primary CSV contains **180,519 rows and 53 columns** at order-item grain: `Order Item Id` is unique, representing **65,752 distinct orders**. Order dates span **2015-01-01 to 2018-01-31**. The raw file also includes customer names, contact information, and addresses, so it is not included in this portfolio package.

## Dashboard walkthrough

The PBIX contains four primary report pages. Page names below are the names stored in the file; descriptions summarize the intended decision questions.

| Page | Decision question | Focus |
|---|---|---|
| **Overview** | How is the business performing overall? | Executive view of business health and performance |
| **Business** | Where are revenue and profit coming from, and how are they changing? | Commercial performance analysis |
| **Operations** | Where are delivery and fulfillment risks concentrated? | Delivery and operational performance |
| **Insight** | Which patterns should leadership act on first? | Year comparison, delivery-risk findings, and recommendations |

The PBIX also contains a tooltip page and two hidden pages. Screenshots are not included yet; add sanitized page captures here before using the repository as a final public portfolio link.

## Data model and analytical approach

The report metadata references a central `Fact_OrderLine` table alongside `Dim_Customer`, `Dim_Date`, `Dim_Delivery`, `Dim_Geography`, `Dim_Product`, and `_Measure`, plus parameter tables. This resembles a sales and operations model organized around order-line facts and customer, date, delivery, geography, and product dimensions.

The exact relationships, cardinalities, filter directions, date-table configuration, Power Query steps, and DAX formulas have not been independently confirmed. The findings below are recalculated from the source CSV using explicit candidate definitions; they should not be read as proof of the report's exact DAX or current filter state.

### KPI definitions used for reconciliation

| KPI | Reconciliation definition |
|---|---|
| Sales | Sum of source `Sales` at order-item grain |
| Orders | Distinct count of `Order Id` |
| Sales per order | Sales divided by distinct orders |
| Late orders | Distinct orders with late delivery status |
| Late-sales share | Sales on late-status order-item rows divided by total Sales |

## Findings from the source data

These figures were recalculated from the provided source CSV. Sales values are shown without a currency symbol because the report's currency definition has not been verified.

- **Sales total:** 36.785M, consistent with the report's displayed 36.78M at its shown precision.
- **2017 vs. 2016:** distinct orders increased **4.83%**, while Sales decreased **4.03%** and Sales per order decreased **8.45%**. This indicates lower sales value per order over that comparison period; the data alone does not identify the cause.
- **Revenue concentration:** the three largest departments account for **80.74%** of Sales, indicating substantial concentration in the largest categories.
- **Delivery exposure:** **36,048 of 65,752 orders (54.82%)** were late. Late-status order-item rows represent **54.71%** of Sales.
- **Mode-specific exposure:** Standard Class accounts for **14,995 distinct late orders** and **8.365M late Sales**. Fan Shop late Sales total **9.377M**. First Class late rate is **95.27% by distinct orders** (95.32% by order-item rows).

Delivery Status and `Late_delivery_risk` agree across all source rows checked. These associations identify where to investigate; they do not establish why delays occurred.

## Recommendations for leadership

1. **Investigate the drop in sales per order.** Break the 2017 movement down by product, department, customer segment, and geography; test pricing, product mix, and order composition before choosing an intervention.
2. **Protect concentrated revenue and develop other contributors.** Track the largest departments while assessing whether smaller departments have credible growth opportunities.
3. **Prioritize delivery improvement by exposure and rate.** Review Standard Class volume and late sales alongside the very high First Class late rate. Segment by geography, product, and time to locate operational drivers, then assign owners and measurable service targets.

These are hypotheses and follow-up actions based on the observed patterns, not causal conclusions.

## Tools and skills demonstrated

- **Power BI Desktop:** multi-page executive report and interactive analysis.
- **DAX:** report measures and period comparisons are present in the PBIX; formulas need a final review before publishing exact definitions.
- **Data analysis:** source profiling, distinct-order versus order-item grain checks, KPI reconciliation, and consistency checks for delivery fields.
- **Communication:** translating commercial and operational patterns into stakeholder questions and prioritized next steps.

Custom Pareto and Sankey visuals are embedded in the PBIX. Power BI Desktop version and exact Power Query transformations have not been documented.

## How to review the project

The local PBIX is `report/K47_Nguyen Xuan Thu_Project4.pbix`. It is excluded from Git because it may embed the customer-level source data. It will not be available in a GitHub clone. For a public application, include sanitized screenshots or an approved Power BI viewing link after checking access settings and data exposure. No screenshots or public report link are included yet.

The repository also contains project notes and a KPI reconciliation notebook for deeper review. The README is the main portfolio overview; those materials are optional supporting evidence.

## Limitations and sharing notes

- The PBIX visual rendering, interactive behavior, current filters, DAX formulas, model relationships, and currency have not been fully reviewed in Power BI Desktop.
- The reconciliation uses candidate definitions stated above. Report totals align at displayed precision, but this does not guarantee every visual uses the same filters or aggregation.
- The source dataset includes personally identifying customer fields. Do not publish the raw CSV, customer-level extracts, credentials, or connection details. The repository `.gitignore` excludes common data files and the PBIX by default.
- Attribute the dataset and follow the source license for any material redistributed with this project.

## Project structure

```text
dataco-supply-chain-portfolio/
├── README.md             # Recruiter-facing project overview
├── .gitignore            # Excludes PBIX, raw data, and local/private files
├── assets/               # Supporting visual assets
├── data_sample/          # Reserved for a sanitized, approved sample only
├── docs/                 # Detailed project and report notes
├── notebooks/            # KPI reconciliation notebook
├── report/               # Local PBIX; ignored by Git
└── screenshots/          # Add sanitized dashboard captures before sharing
```
