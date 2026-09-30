# ChurnInsight - Customer Churn Analysis

An end-to-end customer churn analysis project that combines subscription history, customer demographic data, and customer support ticket logs to understand why customers cancel and measure financial impact.

## Overview

Retaining customers is critical for subscription-based businesses. This project processes raw customer and support data, models it in a local SQLite database, prepares a consolidated analytical dataset, and evaluates key churn metrics and behavioral patterns.

The analysis answers fundamental business questions:
- What is the overall churn rate and retention rate?
- Which subscription plans and contract durations experience the highest attrition?
- How much monthly recurring revenue is currently lost to churn (Revenue at Risk)?
- Is there a measurable relationship between support complaints/escalations and churn?
- How can customers be segmented into clear churn risk tiers for proactive retention?

## Workflow

1. Data Ingestion & Storage
   - Reads multiple sheets from `customer_churn_data_raw.xlsx` (customer demographics, subscription events, support tickets).
   - Writes tables to a local SQLite database (`customer_churn.db`) and inspects table schemas dynamically.

2. Data Cleaning & Transformation
   - Standardizes gender categories and formats date attributes (`dob`, `subscription_start_date`, `renewal_date`, `cancellation_date`, `complaint_date`).
   - Removes unused demographic attributes (`interests`, `pincode`).
   - Calculates complaint counts per customer and handles multiple support interactions.
   - Derives binary flags (`churn_flag`, `escalations`).

3. Feature Engineering & Dataset Consolidation
   - Merges customer profiles, subscription lifecycles, and aggregated support histories into a unified table.
   - Computes customer tenure in days.
   - Maps churn scores into risk tiers: Low (< 50), Medium (50 to 69), and High (>= 70).
   - Exports the combined dataset to `exported_churn_data.csv`.

4. Exploratory Data Analysis & Visualizations
   - Calculates core business metrics: Churn Rate, Retention Rate, ARPU (Average Revenue Per User), and Revenue at Risk.
   - Visualizes monthly churn trends over time.
   - Analyzes churn distribution by subscription plan and region.
   - Encodes categorical variables to generate correlation heatmaps and identify key drivers.
   - Produces multi-variable breakdown charts and pivot tables for revenue and volume planning.

## Key Metrics Evaluated

- Churn Rate & Retention Rate: Baseline customer retention health.
- ARPU (Average Revenue Per User): Mean monthly revenue generated per active subscription.
- Revenue at Risk: Total monthly charges associated with churned accounts.
- Average Customer Tenure: Duration in days before cancellation versus active customer lifespan.
- Support Escalation & Complaint Rates: Frequency of customer complaints and their correlation with cancellation behavior.
- Churn Risk Tiers: Customer segmentation into actionable risk groups.

## Project Structure

```
ChurnProject/
|-- main.ipynb                   # Jupyter notebook containing the full analysis pipeline
|-- customer_churn_data_raw.xlsx # Raw source data (demographics, subscriptions, support)
|-- customer_churn.db            # SQLite database generated during ingestion
|-- exported_churn_data.csv      # Cleaned and merged dataset
`-- README.md                    # Project documentation
```

## Getting Started

### Prerequisites

You need Python 3.8+ installed along with the following libraries:

```bash
pip install pandas numpy matplotlib seaborn openpyxl
```

### Running the Notebook

1. Ensure `customer_churn_data_raw.xlsx` is present in the project root directory.
2. Open Jupyter Notebook or JupyterLab:
   ```bash
   jupyter notebook main.ipynb
   ```
3. Run all cells sequentially to ingest the raw data, populate the SQLite database, and run the analysis and charts.
