# YouTube Trending Data Pipeline

## Overview

A cloud-native ETL pipeline that collects YouTube trending video
data using the YouTube Data API, processes the data through a
Medallion Architecture, performs data quality checks, and produces
analytics-ready datasets.

## Architecture

![YouTube Data Pipeline Architecture](architecture/youtube-data-pipeline-architecture.png)

## Data Flow

YouTube Data API
        ↓
AWS EventBridge
        ↓
AWS Step Functions
        ↓
AWS Lambda / Python
        ↓
Amazon S3 - Bronze
        ↓
AWS Lambda / AWS Glue
        ↓
Amazon S3 - Silver
        ↓
Data Quality Checks
        ↓
Amazon S3 - Gold
        ↓
Amazon Athena
        ↓
Amazon QuickSight

## Technologies Used

- Python
- YouTube Data API
- AWS Lambda
- Amazon S3
- AWS Glue
- AWS Step Functions
- Amazon EventBridge
- Amazon Athena
- Amazon QuickSight
- Amazon SNS

## Project Workflow

### 1. Data Ingestion

The pipeline retrieves trending YouTube video information through
the YouTube Data API.

### 2. Bronze Layer

The original API response is stored in Amazon S3 as the raw data layer.

### 3. Silver Layer

The raw data is cleaned and transformed into a structured format.

Operations include:

- Data type standardization
- Handling missing values
- Removing duplicates
- Column standardization

### 4. Data Quality

Quality checks are performed before the data moves to the Gold layer.

Checks include:

- Schema validation
- Null checks
- Duplicate checks
- Data type validation
- Basic business rules

### 5. Gold Layer

Validated data is transformed into business-ready datasets
for analytics.

### 6. Analytics

Amazon Athena is used to query the Gold layer, while Amazon
QuickSight can be used for dashboards and reporting.

### 7. Orchestration

AWS Step Functions manages the sequence of pipeline activities,
while Amazon EventBridge triggers the workflow.

### 8. Error Handling

If a pipeline step or data-quality check fails, the workflow
can stop the downstream processing and send an alert through
Amazon SNS.

## Key Features

- API-based data ingestion
- Cloud-native architecture
- Medallion architecture
- Automated orchestration
- Data quality validation
- Error handling and notifications
- Analytics-ready datasets

## Project Outcome

The pipeline provides a scalable and automated approach for
collecting, processing, validating, and analyzing YouTube
trending data.
