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

*	**Fact Tables:**
*	fact_sales_monthly: Contains transactional sales data, including quantity and net sales.
*	ns_targets_2021: Stores market-level sales targets for performance comparison.

*	**Dimension Tables:**
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


