# AWS-Based Data Pipeline for Spotify Dataset

## Project Overview
This project demonstrates how to build a data pipeline using AWS Glue, Athena, and Power BI. The pipeline extracts, transforms, and loads data from S3 and visualizes insights using Power BI.

## Architecture Diagram
![Architecture Diagram](architecture/architecture_diagram.png)

### Data Flow
1. **S3 (Staging & Datawarehouse)** - Raw CSV files are stored in S3 (staging) and transformed data is stored in another S3 folder (datawarehouse).
2. **AWS Glue (ETL)** - AWS Glue ETL is used to process and clean the data.
3. **AWS Glue Crawler** - Crawlers scan the data and create metadata tables in AWS Glue Data Catalog.
4. **Athena Queries** - Data is queried using AWS Athena and results are stored in S3.
5. **Power BI Connection via ODBC** - Power BI is connected to Athena using ODBC to visualize the processed data.

## Dataset
- **Original Data**: Spotify dataset containing `artists.csv`, `albums.csv`, and `tracks.csv`, stored in `S3://spotify-project/staging/`
- **Transformed Data**: Processed and cleaned data stored in `S3://spotify-project/datawarehouse/`

## Steps Implemented
### 1️⃣ Data Storage in S3
- Uploaded `artists.csv`, `albums.csv`, and `tracks.csv` to the `staging` folder in S3.

### 2️⃣ Data Processing with AWS Glue
- Used AWS Glue to join all three CSV files.
- Dropped unnecessary columns.
- Saved transformed data in `datawarehouse` S3 folder in **Parquet** format for better performance.

### 3️⃣ Metadata Cataloging with AWS Glue Crawler
- Created an AWS Glue Crawler to scan and catalog the transformed data.
- Created a **Glue Database** and tables for Athena queries.

### 4️⃣ Querying with AWS Athena
- Wrote SQL queries in Athena to analyze the data.
- Saved query results in an S3 bucket (`athena-output`).

### 5️⃣ Connecting to Power BI
- Installed **Athena ODBC Driver**.
- Connected Power BI to Athena via ODBC.
- Ran SQL queries and visualized data using a **Pie Chart**.

## Technologies Used
- **AWS Services**: S3, Glue, Athena
- **Data Processing**: AWS Glue ETL
- **Querying**: AWS Athena (SQL)
- **Visualization**: Power BI
- **Storage Format**: CSV (Raw Data), Parquet (Processed Data)
- **Programming Language**: Python (AWS Glue ETL script)

## How to Run This Project
1. **Set up S3 Bucket**
   - Create an S3 bucket (e.g., `spotify-project`).
   - Upload CSV files to `spotify-project/staging/`.

2. **Create AWS Glue Job & Crawler**
   - Define an AWS Glue ETL Job to process data.
   - Configure a Glue Crawler to scan processed data and create metadata tables.

3. **Query Data using AWS Athena**
   - Run SQL queries in Athena to analyze the transformed data.
   - Save query results in `athena-output` S3 bucket.

4. **Connect Athena to Power BI**
   - Install **Amazon Athena ODBC Driver**.
   - Set up an ODBC connection.
   - Load Athena queries into Power BI and create visualizations.

## Repository Structure
```
│── architecture/
│   ├── architecture_diagram.png  # Diagram of data flow
│── data/
│   ├── sample_data/              # Sample CSV files
│── glue_scripts/
│   ├── etl_script.py             # AWS Glue ETL script
│── queries/
│   ├── athena_queries.sql        # SQL queries used in Athena
│── README.md                     # Project documentation
```

## Future Improvements
- Automate the Glue pipeline using **AWS Lambda**.
- Store processed data in **Amazon Redshift** instead of S3.
- Use **Apache Airflow** for better pipeline orchestration.
- Implement **advanced Power BI dashboards** with interactive filters.
