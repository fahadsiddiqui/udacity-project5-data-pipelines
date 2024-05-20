# Data Pipeline with Airflow

## Overview

Sparkify, a music streaming service, has determined it's time to enhance their ETL pipelines with automation and monitoring. After evaluating various options, they've decided to implement Apache Airflow for this purpose.

## Project Description

This project aims to develop a robust data pipeline that is dynamic, comprised of reusable tasks, easily monitored, and supports backfilling. Given the importance of data quality for reliable analytics, the pipeline includes tests to identify any discrepancies in Sparkify's datasets after the ETL processes. The source data is stored in S3 and needs to be processed into Sparkify's data warehouse hosted on Amazon Redshift. The source datasets include JSON logs detailing user activity within the application and JSON metadata about the songs users listen to.

## Datasets

Here are the S3 links for the datasets used in this project:

- **Log data:** `s3://udacity-dend/log_data`
- **Song data:** `s3://udacity-dend/song_data`

## Structure

The project includes two main directories, `dags` and `plugins`, along with a create tables script and a README file at the root level:
- `create_tables.sql`: SQL script containing the create table statements.

The `dags` directory contains:
- `sparkify_etl_dag.py`: Defines the main DAG, tasks, and their order.

The `plugins/operators` directory contains:
- `stage_redshift.py`: Defines `StageToRedshiftOperator` to copy JSON data from S3 to staging tables in Redshift using the `copy` command.
- `load_dimension.py`: Defines `LoadDimensionOperator` to load dimension tables from staging tables.
- `load_fact.py`: Defines `LoadFactOperator` to load the fact table from staging tables.
- `data_quality.py`: Defines `DataQualityOperator` to run data quality checks on all specified tables.
- `sql_queries.py`: Contains SQL queries for the ETL pipeline.

## Config

This project uses Python 3 and assumes that Apache Airflow is installed and configured.

- Create a Redshift cluster and run `create_tables.sql` once to set up the tables.
- Add the following Airflow connections:
  - AWS credentials, named `aws_credentials`
  - Redshift connection, named `redshift`

## Author

- [Fahad Siddiqui](https://github.com/fahadsiddiqui)
