<h1>
<b>Architecture Diagram </b>
 </h1>

 
<img width="2392" height="844" alt="image" src="https://github.com/user-attachments/assets/659650fa-4ccc-4e76-acab-c147cf8ca80a" />
















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
