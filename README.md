## Description
---
This repo provides the ETL pipeline, to populate the sparkifydb database in AWS Redshift.  
* The purpose of this database is to enable Sparkify to answer business questions it may have of its users, the types of songs they listen to and the artists of those songs using the data that it has in logs and files. The database provides a consistent and reliable source to store this data.

* This source of data will be useful in helping Sparkify reach some of its analytical goals, for example, finding out songs that have highest popularity or times of the day which is high in traffic.

## Why Redshift?
--- 
* Redshift is a fully managed, cloud-based, petabyte-scale data warehouse service by Amazon Web Services (AWS). It is an efficient solution to collect and store all data and enables analysis using various business intelligence tools to acquire new insights for businesses and their customers.  
![Redshift](screenshots/redshift.PNG) 

## Database Design
---
* For the schema design, the STAR schema is used as it simplifies queries and provides fast aggregations of data.
![Schema](screenshots/schema.PNG)

* songplays is our facts table with the rest being our dimension tables.

## Data Pipeline design
* For the ETL pipeline, Python is used as it contains libraries such as pandas, that simplifies data manipulation. It also allows connection to Postgres Database.

* There are 2 types of data involved, song and log data. For song data, it contains information about songs and artists, which we extract from and load into users and artists dimension table

* First, we load song and log data from JSON format in S3 into our staging tables (staging_songs_table and staging_events_table)

* Next, we perform ETL using SQL, from the staging tables to our fact and dimension tables. Below shows the architectural design of this pipeline:
![architecture](screenshots/architecture.PNG)

## Files
---
* create_tables.py is the python script that drops all tables and create all tables (including staging tables)

* sql_queries.py is the python file containing all SQL queries. It is called by create_tables.py and etl.py

* etl.py is the python script that loads data into staging tables, then load data into fact and dimension tables from staging tables

* redshift_cluster_setup.py sets up the redshift cluster and creates an IAM role for redshift to access other AWS services

* redshift_cluster_teardown.py removes the redshift cluster and IAM role created

* dwh.cfg contains configurations for Redshift database. Please edit according to the Redshift cluster and database created on AWS

## Running the ETL Pipeline
---
* First, run create_tables.py to create the data tables using the schema design specified. If tables were created previously, they will be dropped and recreated.

* Next, run etl.py to populate the data tables created.
## Description
---
* This repo contains projects done which applies principles in data engineering. 
* Notes taken during the course can be found in folder `0. Back to Basics`

## Projects
---
1. <ins> Postgres ETL </ins> :heavy_check_mark:
* This project looks at data modelling for a fictitious music startup Sparkify, applying STAR schema to ingest data to simplify queries that answers business questions the product owner may have

2. <ins> Cassandra ETL </ins> :heavy_check_mark:
* Looking at the realm of big data, Cassandra helps to ingest large amounts of data in a NoSQL context. This project adopts a query centric approach in ingesting data into data tables in Cassandra, to answer business questions about a music app

3. <ins> Web Scrapying using Scrapy, MongoDB ETL </ins> :heavy_check_mark:
* In storing semi-structured data, one form to store it in, is in the form of documents. MongoDB makes this possible, with a specific collection containing related documents. Each document contains fields of data which can be queried. 
* In this project, data is scraped from a books listing website using Scrapy. The fields of each book, such as price of a book, ratings, whether it is available is stored in a document in the books collection in MongoDB.

4. <ins> Data Warehousing with AWS Redshift </ins> :heavy_check_mark:
* This project creates a data warehouse, in AWS Redshift. A data warehouse provides a reliable and consistent foundation for users to query and answer some business questions based on requirements.

5. <ins> Data Lake with Spark & AWS S3 </ins> :heavy_check_mark:
* This project creates a data lake, in AWS S3 using Spark. 
* Why create a data lake? A data lake provides a reliable store for large amounts of data, from unstructured to semi-structured and even structured data. In this project, we ingest json files, denormalize them into fact and dimension tables and upload them into a AWS S3 data lake, in the form of parquet files.

6. <ins> Data Pipelining with Airflow </ins> :heavy_check_mark:
* This project schedules data pipelines, to perform ETL from json files in S3 to Redshift using Airflow. 
* Why use Airflow? Airflow allows workflows to be defined as code, they become more maintainable, versionable, testable, and collaborative

7. <ins> Capstone Project </ins> :heavy_check_mark:  
* This project is the finale to Udacity's data engineering nanodegree. Udacity provides a default dataset however I chose to embark on my own project. 
* My project is on building a movies data warehouse, which can be used to build a movies recommendation system, as well as predicting box-office earnings. View the project here: [Movies Data Warehouse](https://github.com/alanchn31/Udacity-Data-Engineering-Capstone)
