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

# Project 2
# Customer Transaction Analytics using Azure & Power BI

## Project Overview
This project demonstrates a **data analytics pipeline** built using **Azure Data Factory (ADF)**, **Azure SQL Database**, and **Power BI** to process and analyze customer transaction data. The goal of the project is to transform raw **CSV data** into actionable business insights, facilitating better decision-making for businesses.

## Project Objectives
1. **Design a scalable data model** for customer transactions.
2. **Ingest raw data** using **Azure Data Factory (ADF)**.
3. **Transform and load** the data into final tables using **Azure SQL Database**.
4. **Create Power BI reports** to visualize customer insights and trends.

## Technologies Used
- **Azure Data Factory (ADF)**: For data ingestion and transformation.
- **Azure SQL Database**: For data storage and transformation.
- **Power BI**: For creating interactive reports and visualizing customer insights.
- **T-SQL**: For data transformation and ensuring referential integrity.

## Project Steps

### 1. Data Modeling
A **star schema** was implemented to structure the data for efficient querying and analysis. The schema includes the following tables:
- **Fact Transaction**: Contains transactional records including amount, date, product, and customer.
- **Dimension Tables**:
  - **DimCustomer**: Stores customer profile information.
  - **DimProduct**: Contains the product catalog.
  - **DimFeedback**: Includes customer feedback responses.
  - **DimReturn**: Tracks return reasons and counts.

This schema ensures fast, flexible analytical queries.

### 2. Data Ingestion with Azure Data Factory
The raw data was ingested using **Azure Data Factory**. A **ForEach activity** was used to loop through multiple datasets and dynamically copy data into staging tables in **Azure SQL Database**.

#### Files Ingested:
- **customersfile.csv** → `Staging_customersfile`
- **products.csv** → `Staging_products`
- **transactionfile.csv** → `Staging_transactionfile`
- **customer_feedback.csv** → `Staging_customer_feedback`
- **transaction_returns.csv** → `Staging_transaction_returns`

#### Ingestion Flow:
- **Source**: **Azure Blob Storage** (CSV files).
- **Destination**: **Azure SQL Database** (Staging Tables).

#### Data Transformation with Azure SQL Database
- Once the data was ingested into staging tables, it was transformed using T-SQL scripts to:
- Rename columns to match the final schema.
- Ensure referential integrity with dimension keys.

Final Tables:
DimCustomer: Customer details.
DimProduct: Product master with category.
FactTransaction: Transaction data (fact table).
DimFeedback: Customer satisfaction ratings.
FactTransactionReturn: Product return data.

#### Power BI Report – Customer Insights
The transformed data was connected to Power BI Desktop using DirectQuery to create interactive reports. The following visuals were created:

Card: Displays total revenue and customer count.
Table: Shows the top 10 customers by spend.
Line Chart: Plots revenue trends over time.
Donut Chart: Breaks down return reasons.
Gauge: Displays the average customer feedback score.

Users can interact with the dashboard to explore:
Customer behavior.
Product performance.
Return trends.
Feedback metrics.

# Conclusion
This project demonstrates how to create a modern cloud-based analytics pipeline using Azure and Power BI to derive valuable insights from customer transaction data. The solution efficiently ingests, transforms, and visualizes data, enabling better business decision-making.

# Project 3
# Healthcare Data Engineering Project using Azure Databricks and Azure SQL Database

## Project Overview
This project aims to build a **scalable and secure data engineering pipeline** for processing healthcare data using **Microsoft Azure** services. The objective is to ingest, transform, and store **patient records** for further analysis and reporting. The project also integrates optional machine learning enhancements for data enrichment.

## Tools and Technologies Used
- **Azure Databricks**: For data processing and transformation using **PySpark**.
- **Azure Data Lake Storage (ADLS)**: To store raw patient data securely.
- **Azure Data Factory (ADF)**: For orchestrating data movement (optional).
- **Azure SQL Database**: As the final destination for the cleaned and transformed data.
- **PySpark / Python**: For scripting data transformations and processing.

## Dataset Description
The dataset contains synthetic **patient information** with the following schema:

- **Name**: String (Patient's name)
- **Age**: Integer (Patient's age)
- **Gender**: String (Patient's gender)
- **Blood Type**: String (Patient's blood type)
- **Medical Condition**: String (Patient's medical condition)
- **Date of Admission**: Date (Date patient was admitted)
- **Doctor**: String (Doctor assigned to the patient)
- **Hospital**: String (Hospital where the patient is admitted)
- **Insurance Provider**: String (Insurance provider for the patient)
- **Billing Amount**: Double (Amount billed for treatment)
- **Room Number**: Integer (Patient's room number)
- **Admission Type**: String (Type of admission)
- **Discharge Date**: Date (Date of patient discharge)
- **Medication**: String (Medication prescribed)
- **Test Results**: String (Test results for the patient)

## Step-by-Step Process

### Step 1: Data Ingestion
- Mounted **Azure Data Lake Storage (ADLS)** container using **dbutils.fs.mount**.
- Loaded the healthcare dataset (`healthcare_dataset.csv`) into a **PySpark DataFrame** for further processing.

### Step 2: Data Exploration
- **Validated** the schema and data types.
- Checked for **missing/null values**, ensuring there were no missing values in any of the columns.

### Step 3: Data Transformation in Databricks
- Added derived fields to enhance the dataset:
  - **LengthOfStay**: Calculated the number of days between **admission** and **discharge** dates.
  - **HighBillingFlag**: Flagged patients with billing amounts greater than **$10,000**.
  - **AgeGroup**: Categorized patients into three age groups:
    - **Child**: Age < 18
    - **Adult**: Age 18-59
    - **Senior**: Age 60+

### Step 4: Data Export to Azure SQL Database
- Established a **JDBC connection** to **Azure SQL Database** using the SQL Server driver.
- Wrote the transformed **DataFrame** into the **dbo.PatientRecords** table using `.write.jdbc()`.

```python
jdbc_url = "jdbc:sqlserver://divyaproject.database.windows.net:1433;database=YourDatabaseName"
connection_properties = {
    "user": "YourSQLUsername",
    "password": "YourSQLPassword",
    "driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver"
}

# Writing transformed DataFrame to SQL Database
df_transformed.write.jdbc(
    url=jdbc_url,
    table="dbo.PatientRecords",
    mode="overwrite",
    properties=connection_properties
)

Conclusion
This project successfully built a scalable and secure data pipeline using Azure Databricks, Azure Data Factory, and Azure SQL Database to process and store healthcare data. The pipeline efficiently ingests, transforms, and loads patient records, enabling better data analysis and reporting.
