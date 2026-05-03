<h1>
<b>Architecture Diagram </b>
 </h1>

 
<img width="2392" height="844" alt="image" src="https://github.com/user-attachments/assets/659650fa-4ccc-4e76-acab-c147cf8ca80a" />


<b>Project Overview</b>

This project implements an end-to-end data engineering pipeline using Azure Data Factory (ADF) following Medallion Architecture principles. The pipeline ingests data from mixed sources (Azure SQL Database + GitHub HTTP), processes it through Bronze → Silver → Gold layers, and delivers a Power BI dashboard for retail analytics.

<b>Key Features:</b>

Multi-source ingestion (SQL DB + HTTP file)

ADF Mapping Data Flows for transformations

Row count validation and error handling

Azure SQL Database as Gold layer

Power BI sales reporting

<b>Business Problem</b>

The project creates a retail analytics platform by combining:

Transactions, Products, Stores from operational SQL Database

Customers from external GitHub HTTP source

The final Gold layer enables sales trend analysis, top product reporting, and customer insights.


<b> Medallion Architecture</b>

Bronze Layer (ADLS Gen2)
Raw data landed as-is without transformation:

SQL exports as CSV

GitHub HTTP as JSON

No schema enforcement or filtering

<b> Silver Layer (ADLS Gen2)</b>

Cleansed and transformed using ADF Mapping Data Flows:

Null handling

Data type standardization

Business logic applied

Ready for analytics

<b> Gold Layer (Azure SQL Database)</b>
Curated fact/dimension model for reporting:

Joins between Silver datasets

Business calculations (sales_amount = quantity * price)

Final reporting table with relationships











<b>Source Systems</b>


Azure SQL Database: Transactions, Products, and Stores tables are extracted as source data


GitHub HTTP source: Customer data is ingested from a GitHub-hosted file over HTTP.

<b> Flow</b>

SQL source data and GitHub HTTP customer data are landed into the Bronze layer in ADLS as raw data

ADF Mapping Data Flows transform the raw data into Silver curated datasets.

Silver datasets are joined and enriched into a final Gold reporting table in Azure SQL for analytics and reporting.

<b> Architecture line</b>

Azure SQL DB (Transactions, Products, Stores) + GitHub HTTP (Customers) -> ADLS Bronze -> ADF Data Flows -> ADLS Silver -> Azure SQL Gold -> Power BI/Fabric

<b>Data Pipeline Overview</b>

1. Extract Transactions, Products, and Stores from Azure SQL Database.
2. Extract Customers data from GitHub HTTP source.
3. Land all raw data into the Bronze layer in ADLS Gen2.
4. Transform and cleanse data into the Silver layer using ADF Mapping Data Flows.
5. Join Silver datasets to create the final Gold reporting table.
6. Load the Gold table into Azure SQL Database.
7. Build reports in Power BI / Microsoft Fabric for analytics and sales reporting.


<b> Data Validation </b>


Row Count Checks implemented in pipeline:

Bronze input vs Silver output

Silver input vs Gold output

Rejected rows logged

Pipeline JSON Validation:

ADF Studio validation before publish

All datasets/linked services resolved

No broken mappings


<b> How to Run </b>


<b> Prerequisites </b>


Azure subscription

ADF instance

ADLS Gen2 account

Azure SQL Database

Power BI Desktop or Fabric

<b> Deployment Steps </b>



Deploy ADF pipelines/dataflows (ARM templates or manual)

Create Azure SQL tables

Update linked service credentials

Trigger pl_master_pipeline

Connect Power BI to Azure SQL


<b>Dashboard </b>

<img width="784" height="445" alt="Screenshot 2026-05-03 at 7 21 55 PM" src="https://github.com/user-attachments/assets/321ab27c-63cc-4c82-a9ff-916127adae68" />










This project analyses sales by category,city and time.The dashbaord highlights the top-selling category,the best-performing city and allows year/quarter drill-down analysis.

Sales are strongest in Electronics and Mumbai,and the report supports analysis by year and quarter.
