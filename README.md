# Real-Time SaaS Usage Analytics Pipeline (Azure)

## Overview

This project demonstrates an end-to-end real-time data engineering pipeline
for a product-based SaaS company.

The pipeline ingests streaming user activity events, processes them using
Apache Spark on Azure Databricks, and stores curated data in Azure Synapse
Analytics for downstream reporting and analytics.

The goal of this project is to showcase production-style data engineering
practices, including streaming ingestion, medallion architecture, and
analytics-ready data modeling.

## Business Problem

Modern SaaS companies rely heavily on product usage data to understand how
users interact with their applications.

Key questions include:
- Which features are most actively used?
- How does user engagement differ between free and paid plans?
- How does usage evolve over time?

Raw event data is high-volume, unstructured, and arrives in real time.
Without a reliable data pipeline, product and analytics teams cannot generate
timely insights.

This project simulates a real-world SaaS analytics use case and builds a
scalable data platform to address these challenges.

## Architecture

The pipeline follows a streaming-first architecture using Azure-native
services.

User activity events are produced continuously and sent to Azure Event Hub.
Azure Databricks consumes the event stream and processes the data using a
multi-layered medallion architecture (Bronze, Silver, Gold).

Curated, analytics-ready data is stored in Azure Synapse Analytics and can be
consumed by BI tools such as Power BI.

## Data Flow

1. A Python-based event simulator generates SaaS user activity events
   (logins, feature interactions, session endings).
2. Events are streamed in real time to Azure Event Hub.
3. Azure Databricks reads the event stream and writes raw data to the Bronze
   layer in Azure Data Lake Storage.
4. Silver layer transformations clean, validate, and deduplicate events.
5. Gold layer transformations aggregate data and create fact and dimension
   tables using a star schema.
6. Gold tables are loaded into Azure Synapse Analytics for reporting.

## Technology Choices

- **Azure Event Hub**: Used for scalable real-time event ingestion.
- **Azure Databricks (Apache Spark)**: Used for distributed stream processing
  and transformation.
- **Azure Data Lake Storage Gen2**: Acts as durable storage for Bronze, Silver,
  and Gold layers.
- **Azure Synapse Analytics**: Serves as the analytical data warehouse.
- **Python**: Used for event simulation and orchestration logic.
- **Git/GitHub**: Version control and project collaboration.

## Project Structure

real-time-saas-usage-azure/
├── simulator/            # Event generation scripts
├── databricks/           # PySpark transformation jobs
├── synapse/              # SQL DDL for star schema
├── architecture/         # Architecture diagrams
└── README.md

## How to Run Locally

The event simulator can be run locally using Python.

Azure services such as Event Hub, Databricks, and Synapse require an Azure
subscription. This repository focuses on code structure and design rather
than full local emulation of cloud services.

## Cloud Deployment Notes

This project is designed to run on Azure using free-tier or trial resources.

All credentials and connection strings are expected to be provided via
environment variables or secret scopes and are intentionally excluded from
this repository.

## Future Improvements

- Add automated data quality checks
- Implement late-arriving event handling with watermarks
- Introduce orchestration using Apache Airflow
- Extend the pipeline to support Snowflake or BigQuery
- Add CI checks for SQL and Spark code
