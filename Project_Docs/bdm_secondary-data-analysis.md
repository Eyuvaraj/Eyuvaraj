# Business Data Management Capstone: Seasonal Demand Planning and Supplier Concentration Risk

**Project:** Seasonal Demand Planning and Supplier Concentration Risk in State-Regulated Convenience Liquor Retail: An Analysis of Iowa Wholesale Transaction Data

**Repository:** https://github.com/Eyuvaraj/demand-supplier-analysis.git

**Course:** BSMS2001P, Business Data Management Project

**Institution:** Indian Institute of Technology Madras

**Program:** BS in Data Science and Applications

**Project Period:** May to September 2026

**Project Type:** Independent business research and data analytics

**Data Collection Approach:** Secondary data analysis

## One-line Summary

Independent business analytics project analyzing five years of publicly available Iowa Alcoholic Beverages Division wholesale liquor transaction data for Casey's General Stores locations in Iowa, using time-series analysis, seasonal indices, category performance analysis, vendor concentration metrics, and store-level revenue distribution to derive inventory planning and product portfolio insights.

## Project Context

The project was completed as part of BSMS2001P, the Business Data Management Capstone Project, within the IIT Madras BS in Data Science and Applications program.

The objective was to investigate a practical business problem, prepare and analyze relevant data, interpret findings in a business context, and develop actionable recommendations for decision-makers.

The project followed the **secondary-data route**. Rather than collecting primary data through direct business interviews or field visits, the analysis used an existing public dataset published by the Iowa Alcoholic Beverages Division (ABD), the state agency responsible for Iowa's liquor distribution system.

The study focused on Casey's General Stores' Iowa liquor purchasing activity, examining two areas:

1. Seasonal demand patterns and their implications for inventory planning.
2. Product category and supplier concentration, with a focus on portfolio strategy and purchasing dependency.

The work was conducted as an independent academic analysis. It was not commissioned by Casey's General Stores, and no access to the company's internal systems, procurement policies, or management data was available.

## Business Problem

### Problem 1: Seasonal Demand Planning

Wholesale purchasing activity displayed recurring monthly patterns across the five-year analysis period. However, the public transaction data does not establish whether Casey's uses a formal seasonal demand model internally.

The project therefore aimed to quantify these patterns and develop an evidence-based reference calendar for potential procurement and inventory planning.

Key questions:

* Is monthly liquor purchasing seasonality consistent across multiple years?
* Which months exhibit above-average or below-average revenue?
* How large is the difference between peak and trough months?
* How could seasonal patterns inform purchasing schedules and inventory allocation?

### Problem 2: Product Portfolio and Supplier Concentration

A relatively small number of product categories and suppliers accounted for a substantial proportion of total wholesale purchasing revenue.

The project aimed to quantify this concentration, examine category-level growth over time, and identify areas where product assortment and supplier dependency warranted further review.

Key questions:

* Which product categories contribute most to revenue?
* Which categories are growing, stagnating, or declining?
* How concentrated is revenue across wholesale vendors?
* What does supplier concentration imply about potential exposure to supply disruption?
* How does purchasing revenue vary across individual stores?

These are analytical questions derived from public transaction data, not confirmed diagnoses of Casey's internal procurement practices.

## Data Source and Provenance

**Publisher:** Iowa Alcoholic Beverages Division (Iowa ABD)

**Dataset:** Iowa Liquor Sales

**Public data portal:** https://data.iowa.gov/catalog/dataset/1072

**Data access date:** 9 June 2026

**Original format:** CSV

**Analysis period:** January 2021 to December 2025

The dataset records wholesale liquor transactions processed through Iowa's state distribution system. Each row represents a product line within a store order and includes information about the store, product, supplier, order date, quantity, and sales value.

The analysis filtered the public dataset to transactions whose store name contained `CASEY'S`, then restricted the records to the five calendar years from 2021 through 2025.

The project is an independent analysis of publicly available administrative transaction data. Casey's General Stores did not provide the dataset directly, and the findings should not be interpreted as verified information about the company's internal operations.

## Dataset Scale

| Attribute                   |           Value |
| --------------------------- | --------------: |
| Full downloaded dataset     |  2,028,780 rows |
| Columns in original dataset |              21 |
| Filtered analysis dataset   |  1,332,340 rows |
| Analysis period             |    2021 to 2025 |
| Unique store numbers        |             570 |
| Product categories          |              48 |
| Vendors or suppliers        |             155 |
| Product SKUs                |           3,088 |
| Revenue measure             | `sales_dollars` |

The analysis operates at the transaction-line level. An invoice may contain multiple product lines, so `invoice_id` is not treated as a unique row identifier.

The dataset includes transaction dates, store identifiers and locations, product descriptions, categories, vendors, bottle quantities, bottle volumes, and sales values.

## Technology Stack

**Programming language**

* Python

**Data manipulation and analysis**

* Pandas
* NumPy

**Visualization**

* Matplotlib

**Development environment**

* Jupyter Notebook
* Google Colab

**Data format**

* CSV

The reproducible notebook contains the data loading, cleaning, analytical calculations, validation checks, visualizations, and results underlying the final report.

**Notebook:** https://colab.research.google.com/drive/1wodVyUFgagaJaOmmb9qcYMEtkl5SG4E8?usp=sharing

## Analytical Methodology

### 1. Data Loading, Filtering, and Quality Assessment

Loaded the Iowa Liquor Sales dataset and isolated Casey's store transactions for the 2021 to 2025 analysis window.

The workflow examined dataset dimensions, data types, missing values, numerical distributions, and the consistency of key analytical variables.

Important data characteristics included:

* 1,332,340 transaction-line records in the analysis window.
* 221 missing values in `county_name`, approximately 0.02% of records.
* 940 records with negative sales quantities, approximately 0.07% of records, representing returns and credit adjustments.
* No missing values in the primary analytical variables identified in the report: `sales_dollars`, `category_name`, `vendor_name`, and `ordered_on`.

Negative transactions were retained in the final report's descriptive statistics because they represent genuine commercial activity. Data preparation and analytical calculations were documented in the notebook.

### 2. Annual Revenue Trend Analysis

Aggregated sales revenue by calendar year and calculated year-on-year growth.

The analysis also examined average revenue per transaction to distinguish changes in overall revenue from changes in average transaction value.

**Purpose:** Identify long-term revenue trends, changes in growth rates, and potential shifts in purchasing value.

### 3. Monthly Seasonality Analysis

Compared monthly revenue across five separate years, from 2021 through 2025.

A multi-year comparison was used to identify recurring monthly patterns rather than relying on a single year's observations.

Calculated a monthly seasonal index using:

`Seasonal Index = Average revenue for a given month across years / Overall average monthly revenue`

An index above 1.0 indicates revenue above the overall monthly average; an index below 1.0 indicates revenue below that average.

**Purpose:** Quantify recurring seasonal patterns and translate them into a potential planning calendar.

### 4. Product Category Performance

Ranked all 48 product categories by cumulative revenue over the five-year period.

Compared annual revenue for the five highest-revenue categories to identify growth patterns, relative performance, and possible changes in the product portfolio.

**Purpose:** Identify the categories that drive revenue and those showing particularly strong growth or signs of stagnation.

### 5. Vendor Concentration Analysis

Calculated each vendor's share of total five-year revenue and examined cumulative supplier concentration.

Used the Herfindahl-Hirschman Index (HHI) to quantify concentration across the vendor base:

`HHI = Sum of squared vendor revenue shares, expressed as percentages`

The analysis used the conventional HHI scale, with values below 1,500 classified as unconcentrated, 1,500 to 2,500 as moderately concentrated, and above 2,500 as highly concentrated.

**Purpose:** Establish a quantitative measure of supplier concentration and identify purchasing dependency that may warrant further investigation.

### 6. Store Revenue Distribution

Aggregated five-year revenue for each of the 570 stores and examined the distribution across the store network.

**Purpose:** Determine whether network-wide averages adequately represent the variation in purchasing activity between stores and assess the potential value of differentiated inventory policies.

## Key Findings

### 1. Annual Revenue Trend

* Total revenue over the five-year analysis period was approximately **$155.0 million**.
* Annual revenue increased from approximately $23.5 million in 2021 to $35.5 million in 2024.
* Revenue growth slowed from 21.6% in 2022 to 7.3% in 2024.
* Revenue declined by 3.5% in 2025.
* Average revenue per transaction fell from $123.76 in 2024 to $119.02 in 2025, while annual transaction counts remained broadly stable.

The 2025 decline therefore coincided with lower average transaction value rather than a substantial reduction in transaction count. Further data would be required to determine whether this represented a temporary change or a sustained trend.

### 2. Recurring Seasonal Demand

The monthly analysis revealed two recurring periods of elevated revenue: June and the fourth quarter.

| Month    | Seasonal index | Deviation from average |
| -------- | -------------: | ---------------------: |
| February |          0.802 |                 -19.8% |
| January  |          0.861 |                 -13.9% |
| June     |          1.126 |                 +12.6% |
| October  |          1.091 |                  +9.1% |
| November |          1.092 |                  +9.2% |
| December |          1.098 |                  +9.8% |

June was the strongest month relative to the overall monthly average, while February was the weakest.

The ratio of the June seasonal index to February's index was approximately **1.40**, indicating a 40% difference between the peak-month and trough-month indices.

At the quarterly level, Q4 accounted for 27.3% of annual revenue, compared with 21.2% for Q1.

### 3. Product Category Performance

The five highest-revenue categories collectively accounted for approximately 70% of total five-year revenue.

| Category                  | Revenue growth, 2021 to 2025 |
| ------------------------- | ---------------------------: |
| American Vodkas           |                       +45.5% |
| Whiskey Liqueur           |                       +74.5% |
| Canadian Whiskies         |                       +19.1% |
| Spiced Rum                |                         0.0% |
| Straight Bourbon Whiskies |                      +108.3% |

American Vodkas remained the largest category by revenue. Whiskey Liqueur showed strong growth, while Straight Bourbon Whiskies more than doubled in revenue over the period.

Spiced Rum recorded flat growth across the beginning and end of the analysis window, suggesting that its product assortment and performance could be examined further.

The report also identified 100% Agave Tequila as a rapidly growing category, with reported growth of 163.6% over the period.

### 4. Vendor Concentration

* The two largest vendors accounted for **48.6% of total five-year revenue**.
* Sazerac Company Inc. represented approximately 28.1% of revenue.
* Diageo Americas represented approximately 20.5%.
* The top five vendors accounted for approximately 70.0% of revenue.
* The top ten vendors accounted for approximately 86.0%.
* The calculated HHI was **1,444**, just below the conventional 1,500 threshold for moderate concentration.

Although the HHI fell within the unconcentrated range under the benchmark used, the share represented by the largest individual suppliers remains relevant when assessing buyer-level dependency.

A market-wide concentration metric does not, by itself, establish the actual disruption risk faced by an individual retailer.

### 5. Store Revenue Distribution

The analysis covered 570 store locations and found a **443-fold difference between the highest and lowest cumulative store revenue** over the five-year window.

This substantial variation indicates that a single inventory policy based on a network-wide average may not adequately reflect the different purchasing scales of individual outlets.

The report also found that 42.1% of stores in the bottom revenue decile were recently opened, highlighting the importance of accounting for store age and operating history before interpreting low cumulative revenue as weak underlying demand.

## Business Interpretation and Recommendations

The recommendations were derived from the observed patterns and are proposed actions for further consideration, not confirmed operational decisions or implemented changes at Casey's.

### 1. Seasonal Inventory Planning

* **Prepare for the June peak:** Evaluate replenishment schedules ahead of June, particularly for high-revenue, high-velocity categories.
* **Plan for the fourth-quarter peak:** Review purchasing requirements before October to December, when revenue consistently exceeded the monthly average.
* **Manage the winter trough:** Consider lower replenishment requirements during January and February, subject to actual inventory, shelf availability, and local demand.
* **Differentiate inventory by store tier:** Develop store-level demand baselines instead of applying identical inventory targets across outlets with substantially different sales volumes.

### 2. Product Portfolio Strategy

* Review opportunities to expand the assortment of growing categories, particularly Straight Bourbon Whiskies and 100% Agave Tequila.
* Investigate the strong growth in Whiskey Liqueur and the continued revenue contribution of American Vodkas.
* Review Spiced Rum's flat five-year growth to determine whether individual products or the broader category require further analysis.
* Examine bottle-size preferences, including the substantial revenue contribution of 50 ml and 750 ml formats.

### 3. Supplier Concentration Monitoring

* Monitor the revenue share of the largest suppliers over time.
* Evaluate the potential business impact of disruption involving highly represented suppliers.
* Establish a repeatable concentration-reporting process using supplier shares, cumulative revenue percentages, and HHI.
* Distinguish measured concentration from actionable procurement risk, which also depends on contracts, product substitutability, distribution arrangements, and supplier availability.

**Important industry context:** Iowa operates a state-controlled liquor distribution system. Casey's Iowa stores purchase spirits through the Iowa ABD distribution system rather than directly from the producers identified in the transaction records. Recommendations should therefore focus on product assortment, ordering patterns, and exposure to the distribution system, rather than assuming that Casey's can directly negotiate with or replace a producer.

## Project Architecture

This is a notebook-based business analytics project rather than a deployed software application.

The analytical workflow follows:

```text
Public Iowa ABD transaction data
             |
             v
Data loading and filtering
             |
             v
Data quality assessment
             |
             v
Aggregation and feature preparation
             |
             +----------------------+
             |                      |
             v                      v
      Annual and monthly       Category and vendor
      revenue analysis         concentration analysis
             |                      |
             v                      v
      Seasonal index           HHI and revenue shares
             |                      |
             +-----------+----------+
                         |
                         v
               Store-level analysis
                         |
                         v
             Business interpretation
                         |
                         v
           Recommendations and report
```

## Deliverables

The academic project produced the following core deliverables:

* **Proposal report:** Business context, problem definition, objectives, methodology, timeline, and expected outcomes.
* **Analytical notebook:** Reproducible data loading, cleaning, calculations, validation checks, and visualizations.
* **Final report:** Dataset metadata, descriptive statistics, methodology, results, interpretation, and recommendations.
* **Presentation and viva preparation:** Summary of the project approach and key findings.

The notebook and reports document the work. The recommendations were not implemented or independently validated by Casey's management.

## Skills Demonstrated

**Data analytics**

* Data acquisition from a public open-data portal
* Data filtering and quality assessment
* Large CSV processing
* Aggregation and descriptive statistics
* Time-series and seasonal analysis
* Revenue trend analysis
* Category-level performance analysis
* Supplier concentration measurement using HHI
* Store-level distribution analysis

**Business analysis**

* Business problem formulation
* Procurement and inventory planning concepts
* Product portfolio assessment
* Supplier dependency analysis
* Translating analytical results into recommendations
* Communicating assumptions, limitations, and implications

**Technical tools**

* Python
* Pandas
* NumPy
* Matplotlib
* Jupyter Notebook
* Google Colab

## Limitations and Interpretation

* The analysis uses public wholesale transaction records rather than internal retail point-of-sale data.
* Wholesale purchasing activity is a proxy for purchasing demand within the distribution system, not a direct measurement of final consumer sales.
* The data does not establish actual inventory levels, stockouts, wastage, margins, contractual terms, or internal procurement policies.
* Observed seasonality does not establish its underlying cause.
* Revenue concentration does not by itself prove that supply disruption is likely.
* Recommendations are hypotheses for business evaluation, not verified improvements in operational performance.
* The project does not represent a formal consulting engagement with Casey's General Stores.

These limitations define the scope of the conclusions and are important when interpreting the results professionally.

## Academic Context

**Course:** BSMS2001P, Business Data Management Project
**Related course:** BSMS2001, Business Data Management
**Institution:** Indian Institute of Technology Madras
**Program:** BS in Data Science and Applications
**Project period:** May to September 2026

The project applied business and analytical concepts to a real-world dataset, connecting data preparation and quantitative analysis with business interpretation and decision-oriented recommendations.