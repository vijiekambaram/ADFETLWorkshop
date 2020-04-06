# ADF ELT Pipeline

Use case -

Create a simple pipeline to read the file from Windows local folder and load into Sql Server after performing following validations

1. Get the number of files count in Current/Process Folder. If Count <> 1 which means no file or more than one file present, send email notification.

2. If one Current Process File is present, Check File's last modified timestamp, 
  - if day of month >9 Load the Current Process file into Sql Server else load both Current and Previous Process file, send email     notification on count of records loaded
  - Take a backup in Azure Blob.
  - Delete the File from Local Folder.


April 2020

## Target audience

- Data engineers
- Data architects

## Abstracts

### Workshop

At the end of this workshop, you will be better able to build a complete data pipeline using ADF and load into Azure SQL DB/Blob.
In addition, you will learn how to ingest the data, use Azure Data Factory (ADF) for data movement and operationalizing the data pipeline and how to parameterize the pipeline, how to connect to Sources and load into Sql Server, how to store the back up in Azure Data Lake Gen 2, how to send email notification via Logic Apps.


### Hands-on lab

This hands-on lab is designed to provide exposure to many of Microsoft's transformative line of business applications built using Microsoft big data and advanced analytics.

By the end of the lab, you will be able to show an end-to-end solution, leveraging many of these technologies, but not necessarily doing work in every component possible.

## Azure services and related products

- Azure Data Factory (ADF)
- Azure Data Lake Gen2 Storage
- Sql Server or Azure Sql DB
- Azure Logic Apps
- Azure Storage Explorer
