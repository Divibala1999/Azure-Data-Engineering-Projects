# Azure-Data-Engineering-Projects
A collection of hands-on data analytics and engineering projects showcasing end-to-end solutions using Azure, Databricks, Azure Data Factory, Synapse, Power BI, and more.
# Project 1
# Azure Data Pipeline - Customer Account Analysis

## Project Overview
This project demonstrates the creation of a robust **end-to-end data pipeline** in **Azure Data Engineering**. The pipeline ingests raw customer account data, transforms and cleans it using **Azure Databricks**, and finally stores the cleaned data into an **Azure SQL Database** for further analytics. 

The project includes:
- **Data Ingestion**: Using **Azure Data Factory (ADF)** to copy raw data into **Azure Data Lake Storage (ADLS Gen2)**.
- **Data Transformation**: Using **Azure Databricks** with **PySpark** to clean, transform, and process the data.
- **Business Logic**: Apply business logic to calculate customer balances and join datasets.
- **Data Loading**: Persist the transformed data to **Azure SQL Database** for future use.

## Technologies Used
- **Azure Data Factory (ADF)**: Data orchestration for copying data from backend storage to ADLS.
- **Azure Data Lake Storage (ADLS Gen2)**: Raw, curated, and refined data storage (Bronze, Silver, Gold containers).
- **Azure Databricks**: Data transformation using **PySpark**.
- **Azure SQL Database**: Final data storage for analytics and reporting.
- **Apache Spark (PySpark)**: Data cleaning, transformation, and applying business logic.

## Project Steps

### Step 1: Data Ingestion (Backend Storage ➝ Bronze Container)
- **Objective**: Transfer raw data from backend storage into the raw (bronze) container in ADLS.
- **Tool Used**: Azure Data Factory (Copy Activity)
- **Data Sources**: accounts.csv, customers.csv, loan_payments.csv, loans.csv, transactions.csv
- **Sink**: Bronze container in ADLS Gen2

### Step 2: Databricks Activity (Delta Processing on Raw Data)
- **Objective**: Clean and transform raw data for structured storage.
- **Tool Used**: Azure Databricks Notebook (Notebook 1)
- **Operations**:
  - Null handling (remove rows where important fields are missing).
  - Data standardization (e.g., converting address endings like "St" ➝ "Street").
  - Write the transformed data to Parquet/Delta files in the Silver container.

### Step 3: Databricks Activity (ETL from Silver to Gold)
- **Objective**: Apply business logic to generate a refined dataset (customer balances).
- **Tool Used**: Azure Databricks Notebook (Notebook 2)
- **Operations**:
  - Join the accounts with customers dataset.
  - Calculate the total balance for each customer.
  - Write the final dataset into the Gold container as Parquet/Delta files.

### Step 4: Write Transformed Data to Azure SQL Database
- **Objective**: Load the final refined customer data into **Azure SQL Database** for further analytics.
- **Tool Used**: Python (PySpark) for writing to SQL Database
- **Connection**: JDBC connection to Azure SQL Database.
- **Operations**:
  - Read transformed data from Gold container.
  - Write the data into an Azure SQL Database table (`CustomerAccountBalance`).

## Conclusion
This project demonstrates the implementation of a **cloud-based data pipeline** using Azure Data Factory, Azure Databricks, and Azure SQL Database, integrating various Azure services to handle data ingestion, transformation, and storage efficiently.


