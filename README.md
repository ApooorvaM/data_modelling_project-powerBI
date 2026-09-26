# 📊 Power BI End-to-End Data Modeling 

## 📌 Project Overview
In real-world Business Intelligence projects, reporting inaccuracies and performance bottlenecks are rarely caused by complex DAX measures or dashboard designs; they almost always stem from poorly structured underlying data models.

This portfolio project focuses on transforming a **chaotic, nightmare dataset consisting of 23 unorganized tables** into a clean, optimized, enterprise-grade **Star Schema**. The project covers the full end-to-end lifecycle from data exploration, grain evaluation, and Power Query transformations to star schema design, DAX measure engineering, and Row-Level Security (RLS) implementation.

---

## 🎯 Key Project Objectives
1. **Model Optimization**: Re-architect 23 unstructured tables into a robust Star Schema.
2. **Grain Standardization**: Identify entity grains to prevent duplicate records or cross-filtering errors.
3. **Data Hygiene & Standards**: Standardize naming conventions (`dim_` / `fact_` with `snake_case`), set model language to English, and purge unnecessary columns to reduce memory overhead.
4. **Data Protection**: Validate total metrics before and after modeling stages to ensure data integrity.
5. **Security Implementation**: Implement Row-Level Security (RLS) based on regional parameters.

---

## 🛠️ Data Architecture & Modeling Phases

### 1. Exploration & Preparation
- Initial data profiling across all 23 source tables to map entities (B2B Customers, Products, Sales, Inventory, Campaigns, Order Fulfillment).
- Folder structure setup in Power Query for modular tracking and clean query navigation.

### 2. Dimension Modeling (`dim_`)
- Consolidated transactional and descriptive lookup tables into master dimensions:
  - `dim_customer`: Merged customer contact, location, and metadata details while resolving grain mismatch issues.
  - `dim_product`: Cleaned product categories, dropped redundant technical IDs, and structured hierarchies.
  - `dim_date`: Generated an optimized date dimension for time-intelligence reporting.
  - **Junk Dimensions**: Built dedicated dimensions for low-cardinality status attributes and channels.

### 3. Fact Modeling (`fact_`)
- Isolated event-based entities and created core fact tables:
  - `fact_sales` (Header/line item merge, grain alignment, pre-aggregated metric removal)
  - `fact_inventory`
  - `fact_campaign`
  - `fact_order_fulfillment`
- Deactivated non-essential transactional tables to simplify relationship topology.

### 4. Star Schema & DAX Development
- **Relationships**: Configured `1-to-Many` single-direction filters from dimensions to fact tables (avoiding direct fact-to-fact relationships).
- **Core DAX Measures**: Developed calculations inside organized measure folders:
  - Key business metrics: `Total Sales`, `Distinct Order Count`
  - Time-Intelligence: YoY / MoM calculations
  - Operational KPIs: `Order to Pay` duration

### 5. Security & Validation
- Configured dynamic Row-Level Security (RLS) roles for regional data restriction.
- Performed end-to-end sanity checks for circular dependencies, cross-filter directions, and numerical validation.

---

## 📐 Data Model Schema


# 📂 Project Files

| File | Description |
|---|---|
| 📊 [Power BI Data Model](./data_modelling_project.pbix) | Complete Power BI model, transformations, relationships and DAX |
| 📁 [Dataset](./dataset.xlsx) | Original source dataset containing the 23 tables |
| 📝 [README](./README.md) | Project documentation |


# 🔍 Data Modeling: Before vs After

One of the primary objectives of this project was to transform the original unorganized data structure into a clean and optimized Star Schema.

---

## Original Data Model

The original dataset consisted of **23 source tables** with different levels of granularity, overlapping information and complex relationships.

### Original Data Model

<img width="421" height="248" alt="Screenshot 2026-09-26 171149" src="https://github.com/user-attachments/assets/aeadf287-8f7d-422d-b4fe-f1f7169bf86b" />




### Challenges in the Original Model

- 23 source tables
- Different levels of data granularity
- Multiple transactional and lookup tables
- Redundant information
- Complex relationships
- Difficult-to-maintain structure
- Potential aggregation and filtering issues

---

## After — Optimized Star Schema

The source tables were reorganized into a structured dimensional model consisting of **Fact Tables** connected to reusable **Dimension Tables**.

### 🖼️ Final Data Model

<img width="469" height="235" alt="Screenshot 2026-09-26 164110" src="https://github.com/user-attachments/assets/639f7909-5780-4e6a-996a-3506df721000" />




### Improvements

- Clear Fact and Dimension separation
- Standardized table grain
- Consistent naming conventions
- One-to-many relationships
- Single-direction filtering
- Reduced redundancy
- Improved scalability
- Easier DAX development
- Better reporting performance and maintainability

---

# 🏗️ Data Architecture

The final model follows a **Star Schema** architecture.

```text
                    ┌─────────────────┐
                    │   dim_customer  │
                    └────────┬────────┘
                             │
                             │
┌──────────────┐      ┌──────▼───────┐      ┌──────────────┐
│  dim_product │──────│  FACT TABLE  │──────│   dim_date   │
└──────────────┘      └──────┬───────┘      └──────────────┘
                             │
                             │
                    ┌────────▼────────┐
                    │ Supporting Dims │
                    └─────────────────┘
