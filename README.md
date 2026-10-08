A cloud-native ETL pipeline that ingests YouTube trending video data across 10 regions, transforms it through a medallion architecture (Bronze > Silver > Gold), enforces data quality gates, and produces analytics-ready aggregations — all orchestrated by AWS Step Functions.

Architecture:
                         ┌──────────────────────┐
                         │   YouTube Data API   │
                         │  External Data Source│
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │    Amazon EventBridge│
                         │  Scheduled Trigger   │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │   AWS Step Functions │
                         │Pipeline Orchestration│
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │    AWS Lambda /      │
                         │    Python Ingestion  │
                         └──────────┬───────────┘
                                    │
                           Raw API Response
                                    │
                                    ▼
                 ┌─────────────────────────────────┐
                 │          Amazon S3              │
                 │       BRONZE / RAW LAYER        │
                 │  Original YouTube API Data      │
                 └────────────────┬────────────────┘
                                  │
                                  ▼
                 ┌─────────────────────────────────┐
                 │      AWS Lambda / AWS Glue      │
                 │   Data Cleaning & Transformation│
                 └────────────────┬────────────────┘
                                  │
                                  ▼
                 ┌─────────────────────────────────┐
                 │          Amazon S3              │
                 │       SILVER / CLEAN LAYER      │
                 │ Standardized & Validated Data   │
                 └────────────────┬────────────────┘
                                  │
                                  ▼
                 ┌─────────────────────────────────┐
                 │       Data Quality Checks       │
                 │  Nulls • Schema • Duplicates    │
                 │  Data Types • Business Rules    │
                 └───────────────┬─────────────────┘
                                 │
                     ┌───────────┴───────────┐
                     │                       │
                   PASS                    FAIL
                     │                       │
                     ▼                       ▼
        ┌──────────────────────┐   ┌────────────────────┐
        │      S3 GOLD         │   │    Amazon SNS      │
        │ Business-Ready Data  │   │Failure Notification│
        └──────────┬───────────┘   └────────────────────┘
                   │
                   ▼
        ┌──────────────────────┐
        │    Amazon Athena     │
        │ SQL Analytics Layer  │
        └──────────┬───────────┘
                   │
                   ▼
        ┌──────────────────────┐
        │   Amazon QuickSight  │
        │ Dashboards & Reports │
        └──────────────────────┘
