# ADF ELT Pipeline

Use case -

Create a simple pipeline to read the file from Windows local folder and load into Azure SQL DB after performing following validations

1. Get the number of files count in Current/Process Folder. If Count <> 1 which means no file or more than one file present, send email notification.

2. Check File's last modified timestamp, if month >9
- Validate filename of Current/Process File
- Load the file into Azure SQL DB
- Take a backup in Azure Blob
- Delete the File from FTP Folder


April 2020

## Target audience

- Data engineers
- Data architects

## Abstracts

### Workshop

At the end of this workshop, you will be better able to build a complete data pipeline using ADF and load into Azure SQL DB/Blob.
In addition, you will learn how to ingest the data, use Azure Data Factory (ADF) for data movement and operationalizing the data pipeline and how to parameterize the pipeline, how to connect to Sources and load into Azure Sql DB Sink, how to store the back up in Azure Data Lake Gen 2.


### Hands-on lab

This hands-on lab is designed to provide exposure to many of Microsoft's transformative line of business applications built using Microsoft big data and advanced analytics.

By the end of the lab, you will be able to show an end-to-end solution, leveraging many of these technologies, but not necessarily doing work in every component possible.

## Azure services and related products

- Azure Data Factory (ADF)
- Azure Data Lake Gen2 Storage
- Azure Sql DB
- Azure Storage Explorer
- Azure Databricks (Walkthrough)
