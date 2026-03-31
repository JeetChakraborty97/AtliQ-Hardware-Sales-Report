# AtliQ Hardware Sales Analysis Report

<img width="1536" height="1024" alt="Cover Image" src="https://github.com/user-attachments/assets/1a885588-8a60-4566-aeb9-be207947dc8e" />

## Problem Statement

AtliQ Hardware, a fictional company specialising in the manufacturing and sale of hardware products, operates across multiple markets, customers, and product categories. Despite experiencing rapid growth in sales, the company faces challenges in understanding whether this growth translates into optimal business performance.

The management lacks a unified and structured view of their data, making it difficult to:

* Track overall sales performance across regions, customers, and product divisions
* Compare actual sales against predefined targets
* Identify top-performing and underperforming products and customers
* Analyse market-level trends and uncover performance gaps

Additionally, the data is scattered across multiple sources, requiring transformation and modelling before meaningful insights can be derived.

To address these challenges, this project aims to build a structured data model and develop analytical reports that provide clear, data-driven insights into business performance. The goal is to enable stakeholders to make informed decisions by identifying growth opportunities, performance gaps, and areas for optimisation.

# Executive Summary

This report presents a comprehensive analysis of AtliQ Hardware’s sales performance across customers, markets, divisions, and products for the year 2021, using historical comparisons and target benchmarks.

## Data Model & Methodology

The analysis is built using a well-structured Snowflake Schema data model, ensuring efficient querying and scalable reporting.

### Data Model Architecture

**Fact Tables:**
*	fact_sales_monthly: Contains transactional sales data, including quantity and net sales.
*	ns_targets_2021: Stores market-level sales targets for performance comparison.


**Dimension Tables:**
*	dim_customer: Customer details, including platform and channel.
*	dim_product: Product hierarchy (division, segment, category, variant).
*	dim_market: Geographic hierarchy (market, sub-zone, region).
*	dim_date: Time dimension (date, month, fiscal year).

### Relationships

<img width="1248" height="754" alt="Data Model SS" src="https://github.com/user-attachments/assets/10380c96-dd9b-4c27-968d-cf8cdb0604a4" />

The model follows a snowflake schema structure, where normalised dimension tables are interconnected and link to the central fact tables:
* Customer, Product, and Date dimensions are directly linked to the sales fact table.
* Market dimension is connected via both customer and target tables, enabling market-level analysis.
* Date dimension is shared across both sales and target tables, allowing time-based comparisons (actual vs target).

This design enables:
* Multi-dimensional analysis across customers, products, regions, and time
* Efficient aggregation and filtering
* Seamless comparison between actual performance and targets
Overall, the data model ensures high performance, reduced redundancy through normalisation, and strong analytical flexibility, aligning with industry best practices for business intelligence solutions.

## Measures Created

### net_sales
```DAX
=SUM(fact_sales_monthly[net_sales_amount])
```

### net_sales_19
```DAX
=CALCULATE([net_sales], dim_date[fy]="2019")
```

### net_sales_20
```DAX
=CALCULATE([net_sales], dim_date[fy]="2020")
```

### net_sales_21
```DAX
=CALCULATE([net_sales], dim_date[fy]="2021")
```

### target_21
```DAX
=SUM(ns_targets_2021[ns_target])
```

### 2021-Target
```DAX
=[net_sales_21]-[target_21]
```

### 21_vs_20
```DAX
=DIVIDE([net_sales_21]-[net_sales_20], [net_sales_20], 0)
```

### %
```DAX
=DIVIDE([2021-Target],[target_21], 0)
```

## Business Performance Overview

AtliQ Hardware demonstrated exceptional growth in 2021, achieving total net sales of $598.9M, a significant increase from $196.7M in 2020, representing a growth of approximately 204.5%. This indicates strong market expansion, increased demand, and effective sales strategies.

### Market and Geographic Insights

The company’s revenue is highly concentrated in a few key markets. India emerged as the top-performing country with $161.3M in sales, followed by the USA ($87.8M) and South Korea ($49.0M). Despite strong growth across regions, all markets underperformed against targets, with an overall shortfall of $54.9M (-8.4%). This suggests gaps in forecasting accuracy or inefficiencies in execution.

### Customer Performance Analysis

Customer-level analysis reveals robust growth across nearly all channels. Major e-commerce platforms such as Amazon ($82.1M) and AtliQ e-Store ($53.0M) significantly contributed to revenue growth, highlighting the increasing importance of digital sales channels. Several customers demonstrated exponential growth rates exceeding 300%, indicating successful partnerships and market penetration strategies. The total customer net sales grew by 304.5% year-over-year, reinforcing the company’s strong customer acquisition and retention capabilities.

### Product and Portfolio Performance

The product portfolio shows a mixed performance pattern. Top-performing products such as AQ Electron 4 3600 Desktop Processor and AQ Smash 2 recorded exponential growth, contributing significantly to overall revenue. Additionally, new product launches generated $176.2M in revenue, demonstrating successful innovation and product-market fit. However, a small segment of products underperformed, indicating opportunities for portfolio optimisation and discontinuation strategies.

### Division-Level Performance

Among the divisions, the PC division recorded the highest growth rate (313.7%), followed by P&A (221.5%) and N&S (84.4%). This indicates a strong shift toward computing products and accessories, aligning with global digital adoption trends.

## Key Insights and Recommendations

* Strengthen target planning and forecasting processes to reduce performance gaps.
* Continue investing in high-growth markets such as India and the USA while improving performance in underachieving regions.
* Expand and optimise e-commerce channels, as they are major revenue drivers.
* Focus on scaling high-performing products while rationalising underperforming ones.
* Leverage high-growth divisions like PC and P&A for future strategic investments.

## Conclusion

Overall, AtliQ Hardware has achieved outstanding growth in 2021, driven by strong customer expansion, successful product launches, and increasing digital channel penetration. While the company shows significant strengths in scaling and market reach, addressing target gaps and optimising product and regional performance will be critical for sustaining long-term growth.
