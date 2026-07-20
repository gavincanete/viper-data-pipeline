# Viper Data Pipeline

## Project Overview
- This project is a data engineering pipeline that orchestrates multiple ETL (Extract, Transform, Load) processes to collect shoe product data from a target website. Each ETL workflow extracts raw product information, transforms the data through cleaning and validation, and loads the processed records into a PostgreSQL database for storage and analysis.

- The primary goal of the pipeline is to monitor the stock availability of shoes across multiple categories. By automating the collection and processing of inventory data, the pipeline provides a centralized and reliable dataset that can support inventory monitoring, trend analysis, and business decision-making.

## Business Problem
- Monitoring shoe inventory across multiple categories can be time-consuming and error-prone when performed manually. Businesses need accurate and up-to-date stock information to understand product availability, identify low-stock items, and make informed inventory decisions.

- This project addresses that challenge by automating the collection of shoe inventory data. The ETL pipeline extracts stock information from the target website, validates and cleans the data, and stores it in a PostgreSQL database. As a result, businesses have access to a centralized and reliable dataset that reflects the number of available shoes in each category.


## Architecture
- High-level architecture diagram.

<b>Raw Data from Viper Shoe Website:</b> </br>
![Screenshot from 2023-07-21 15-36-05](https://github.com/gavincanete/viper-data-pipeline/assets/33832344/226e3ec3-cf6b-431a-a353-729c64125e1a)

<b>Cleaned and Validated Data</b> </br>
![Screenshot from 2023-07-21 15-35-03](https://github.com/gavincanete/viper-data-pipeline/assets/33832344/cfa07a23-9087-4cb4-bdbc-a291f33391f2)

- Data flow from source to destination.
![viper_data_pipeline](https://github.com/gavincanete/viper-data-pipeline/assets/33832344/369fade7-c978-4607-8763-44ef7cd1571c) </br>
<i>Explanation</i>: </br>
Website → Beautiful Soup (Extraction) → Data Cleaning & Validation → Deduplication → PostgreSQL (Storage) → Pandas (Analysis & Querying)
Apache Airflow orchestrates and schedules the entire pipeline.

## Prerequisites
1) Install the following python packages: </br>
   (requests, beautifulsoup4, pyscopg2, apache-airflow) via pip install <package name> </br>
   ```E.g. pip install configParser```
2) Setting up Postgresql </br>
   ```sudo apt-get install postgresql``` </br>
   ```sudo -i -u postgres``` </br>
   if successfully login, type ```psql``` </br>
   [Output] </br>
   ![Screenshot from 2023-07-20 18-13-14](https://github.com/gavincanete/viper-data-pipeline/assets/33832344/0e43bbe3-a49e-4966-b51e-e5be3246dcbf) </br>
3) Create Shoe Database from Postgresql </br>
   ```create database shoe_db;``` </br>
   ```\c shoe_db``` </br>
    [Output] </br>
    ![Screenshot from 2023-07-20 18-17-23](https://github.com/gavincanete/viper-data-pipeline/assets/33832344/7e734b25-2906-4b3c-9f75-e1134bed819c)

## Setting up Data Pipeline
1) Clone this repository
2) Create <i>shoe_database.ini</i> and place it on the <i>dags folder</i> </br>
   <i>The content of the ini file, should look like this</i></br>
   ![Screenshot from 2023-07-20 19-01-06](https://github.com/gavincanete/viper-data-pipeline/assets/33832344/d1be1dd9-f3c4-4de8-bb58-99185a8ad6a9)
3) Starting the airflow</br>
   ```cd dags/``` </br>
   ```airflow standalone``` (Note: Please change first the path under <i>airflow.cfg</i>)
4) In airflow UI, locate the <i>shoe_dag</i> and run this workflow </br>
   [DAG] </br>
   ![Screenshot from 2023-07-20 19-17-49](https://github.com/gavincanete/viper-data-pipeline/assets/33832344/d06b03d0-4bb5-496c-9f40-1d4b14f94a09)
5) After completion, Open <i>Jupyter Notebook</i> under the <i>dags folder</i>
6) Under Notebook, Select <i>Shoe Visualizer</i>
7) Execute each code provided </br>
   [Output] </br>
   ![Screenshot from 2023-07-21 15-35-29](https://github.com/gavincanete/viper-data-pipeline/assets/33832344/f055e98e-b79b-42e7-9a6c-3e82c8c30df7)

## Technology Stack
- Python
- Airflow
- BeautifulSoup
- PostgreSQL
- Pandas

## Why These Technologies?
### Python
I chose Python because it is the industry standard for data engineering workflows. Its rich ecosystem, including Pandas, NumPy, and PySpark, makes data processing,
transformation, and automation efficient and maintainable.

### Apached Airflow
- Airflow was chosen to orchestrate ETL workflows because:
- Workflows can be represented as code
- Easy scheduling and monitoring
- Industry-wide adoption
- Scalable architecture for future pipelines

### Why BeautifulSoup?
I chose Beautiful Soup because it is one of the most popular and lightweight Python libraries for web scraping. It provides an easy way to parse HTML documents and extract structured data from websites.

### PostgreSQL
I selected PostgreSQL as the data warehouse because it provides:
- Strong SQL compliance
- Excellent analytical query capabilities
- Reliability for production workloads
- Easy integration with ETL tools

### Panda
I chose Pandas because it provides a powerful DataFrame structure for querying, filtering, and analyzing data after it has been loaded into PostgreSQL. Similar to working with SQL tables in tools such as MySQL Workbench, Pandas allows me to efficiently inspect datasets, perform aggregations, and generate insights using Python.

## ETL Pipeline
1. **Extract**
- Scrape product data from a website using Beautiful Soup (BS4).
- Collect raw HTML content and extract relevant fields.
2. **Transform**
- Remove duplicate records to ensure data consistency.
- Validate the data structure and check for missing or invalid values.
- Clean and standardize the dataset using Pandas.
3. **Load**
- Store the processed data in a PostgreSQL database.
- Organize data into structured tables for efficient querying and analysis.
4. **Orchestration**
- Use Apache Airflow to automate and schedule the entire pipeline.
- Monitor task execution and handle workflow dependencies.

## Data Quality
- Duplicate handling
- Missing values
- Validation

## Error Handling
- Retry strategy
- Logging
- Failed scraping

## Scalability
- How would you handle millions of records?
- Parallel scraping
- Incremental loading
- Scheduling

## Future Improvements
- Docker
- CI/CD
- Cloud deploy


   




