![Microsoft Cloud Workshop](https://github.com/vijiekambaram/BigDataWorkshop/blob/master/media/tiger_analytics_logo.PNG 'Microsoft Cloud Workshop')

<div class="MCWHeader1">
Big data Pipeline
</div>

<div class="MCWHeader2">
Hands-on lab step-by-step
</div>

<div class="MCWHeader3">
April 2020
</div>


# ADF ELT Pipeline hands-on lab step-by-step

## Abstract and learning objectives

This hands-on lab is designed to provide exposure to building pipeline using ADF, how to use parameters/variables, how to copy the data from various data sources and load into sink, how to send email notification.

By the end of the lab, you will be able to build an end-to-end pipeline.

## Solution architecture

Below is a diagram of the logic you will build in this lab. Please study this carefully so you understand the whole of the solution as you are working on the various components.

![This is the high-level overview diagram of the end-to-end solution.](./media/logic_flow.png 'High-level overview diagram')

## Requirements

1. Microsoft Azure subscription with permission to create resources.

2. Follow all the steps provided in [Before the Hands-on Lab](Before%20the%20HOL%20-%20ADF%20ETL%20Pipeline.md).

## Exercise 1: Azure Data Factory - Set Up Integration Run Time

1. Go to Azure Data Factory resource created in Before HOL and Click on Author & Monitor.

2. From ADF home page, click on Pencil icon.

   ![ADF Pencil.](./media/exercise_1_adf_pencil.png 'ADF Pencil Icon')
     
3. In order to connect to private network which is not accessible by outside world, we need to have Self Hosted Integration run time. Here we will see how to connect to local folder using Self Hosted IR.

   a.	Click on Connections at the bottom.

  ![ADF Pencil.](./media/exercise_1_IR_Connections.png 'ADF IR Connection Icon')
   
   b. Click on Integration runtimes and then New.

  ![ADF Pencil.](./media/exercise_1_IR_Click.png 'ADF IR Connection Icon') 
   
   c. Click on Azure, Self-Hosted -> Continue.

  ![ADF Pencil.](./media/exercise_1_azure_self_hosted.png 'ADF IR Connection Icon')
 
   d. Select Self Hosted and then Continue.

  ![ADF Pencil.](./media/exercise_1_setup_self_hosted.png 'ADF IR Connection Icon')
   
   e. Enter the details as below i.e Name as SelfHostedForLocal and Description as To Connect to Local and click on Create.

  ![ADF Pencil.](./media/exercise_1_IR_enter_details.png 'ADF IR Connection Icon')

   f.	Click on Option 1 for express set up.

  ![ADF Pencil.](./media/exercise_1_express_setup.png 'ADF IR Connection Icon')
   
   g.	Click on the Link in Option1 to download the integration run time. Copy and paste the authentication key in case of Option2.

   h.	Download the self-hosted integration runtime on a local Windows machine. Run the installer. It will take few minutes for set up.

  ![ADF Pencil.](./media/exercise_1_run_express_setup.png 'ADF IR Connection Icon')
   
   i.	Once it is done, it gets listed under Nodes tab of the IR.

  ![ADF Pencil.](./media/exercise_1_node_ready.png 'ADF IR Connection Icon')
   

## Exercise 2: Azure Data Factory - Linked Services for Local Folder

This exercise is to create connections to connect to Local folder.

1.	Create Linked Service to connect to Local Folder.

2.	Click on Connections -> Linked Services -> New.

3.	Click on File and select File System.

   ![ADF Pencil.](./media/exercise_2_ls_select_fs.png 'ADF IR Connection Icon')

4.	Download the BCTL Zip files sent via email into Local folder. Copy the path of Local Folder as follows.

   ![ADF Pencil.](./media/exercise_2_local_folder_structure.png 'ADF IR Connection Icon')
   
5.	Enter the name as LocalFileServer, IR as SelfHostedForLocal, Host as your local directory that is copied in previous step i.e, Username as your DOMAIN\Windows login, Password as Windows login Password. Click on Test Connection and then Create.

   ![ADF Pencil.](./media/exercise_2_ls_enter_details.png 'ADF IR Connection Icon')
   

## Exercise 3: Azure Data Factory - Dataset for Local Folder

Dataset is use to define the folder name, file type etc.

1. Click on Datasets (…) and select New Dataset.

   ![ADF Pencil.](./media/exercise_3_create_new_dataset.png 'ADF IR Connection Icon')
   
2.  Click on File, Select File System. Click Continue.

   ![ADF Pencil.](./media/exercise_3_ds_select_fs.png 'ADF IR Connection Icon')
      
3. Select the format of file as Delimited Text.

   ![ADF Pencil.](./media/exercise_3_ds_select_file_format.png 'ADF IR Connection Icon')
   
4. Enter the details as follows

   a. Name as SourceProcessFolder.
   
   b. Linked Service as LocalFileServer.
   
   c. First Row as Header – Checked.
   
   d. Import Schema – From Connection/Store.
   
   e. Click Ok.
   
   ![ADF Pencil.](./media/exercise_3_ds_enter_details.png 'ADF IR Connection Icon')

## Exercise 4: Azure Data Factory - Adding Parameters to SourceProcessFolder Dataset

Since this is a common connection for both Current and Previous file, we will add parameters and pass the folder name and file name dynamically depending on which file to read.

1.	Click on Parameters and add parameter foldername  and filename.

   ![ADF Pencil.](./media/exercise_4_add_parameters.png 'ADF IR Connection Icon')

2.	Click on Connection tab and click on Add dynamic content under Directory.

   ![ADF Pencil.](./media/exercise_4_add_connections.png 'ADF IR Connection Icon')
  
3. Select the Foldername parameter created. Click on Finish.

   ![ADF Pencil.](./media/exercise_4_add_foldername_parameters.png 'ADF IR Connection Icon')
   
4. Similarly Add Dynamic Content for filename.

5. Select filename parameter created. Click on Finish.

   ![ADF Pencil.](./media/exercise_4_add_filename_parameters.png 'ADF IR Connection Icon')
   
6. Set the Column delimiter as \t as input file is tab delimited.

   ![ADF Pencil.](./media/exercise_4_column_delimiter.png 'ADF IR Connection Icon')

7.	Click on Drop down in Preview data and select From Files *.

   ![ADF Pencil.](./media/exercise_4_preview_data.png 'ADF IR Connection Icon')
   
8. Provide the value for the parameters foldername as CURRENT\Process and filename as K2_SD_COPA_CURRENT_20191116005603942. Click OK.
   
   ![ADF Pencil.](./media/exercise_4_enter_parameters.png 'ADF IR Connection Icon') 
   
9. Data is shown on the screen. This helps to validate if the settings are fine.

   ![ADF Pencil.](./media/exercise_4_view_data.png 'ADF IR Connection Icon') 

10. Click on Validate All at the top to validate the changes.
   
   ![ADF Pencil.](./media/exercise_4_validate_all.png 'ADF IR Connection Icon') 

11. Click on Publish All on the top to save the changes.
   
   ![ADF Pencil.](./media/exercise_4_publish_all.png 'ADF IR Connection Icon') 
    
## Exercise 5: Azure Data Factory - Linked Services for Sql Server

1. Create Linked Service to connect to Local Folder.

2. Click on Connections -> Linked Services -> New.

3. From Database, scroll down, Click on Sql Server or Azure SQL DB whichever is setup during before HOL. Here we will select Sql Server.
   
   ![ADF Pencil.](./media/exercise_5_select_sql_server.png 'ADF IR Connection Icon') 
   
4. Fill in the details.

   a. Enter the name as LocalSqlServer.
   
   b. Connect via Integration run time-> AutoResolveIntegrationRuntime for Cloud hosted and Selfhosted for Onpremise or private network.
   
   c. Enter the Servername.
   
   d. Enter the databasename as tempdb.
   
   e. Authentication Type as SQL Authentication for Azure SQL DB or already installed existing Sql Server. Use Windows Authentication type for local installation.
   
   f. Enter the Username and Password.
   
   g. Click on Test Connection and Create.
   
   ![ADF Pencil.](./media/exercise_5_enter_details_sql_server.png 'ADF IR Connection Icon') 
   
## Exercise 6: Azure Data Factory - Dataset for Sql Server

1. Click on Datasets (…) and select New Dataset.

2. From Database, scroll down, Click on Sql Server.

3. Enter the name as OutputSqltable, select Linked Service as LocalSqlServer.

4. Tablename as None.

5. Import Schema as None.

6. Click OK.
   
   ![ADF Pencil.](./media/exercise_6_enter_details_sql_server.png 'ADF IR Connection Icon') 
   
## Exercise 7: Azure Data Factory - Adding Parameters to OutputSqltable Dataset

Since this a common connection to the sql server, we can dynamically pass the schema name and table names as parameters.

1.	Click on Parameters and add parameters as tablename and schemaname.

   ![ADF Pencil.](./media/exercise_7_add_parameters.png 'ADF IR Connection Icon') 
   
2.	Click on Parameters and add parameters as tablename and schemaname.

   ![ADF Pencil.](./media/exercise_7_add_connections.png 'ADF IR Connection Icon') 
   
3.	Go to Connection tab and check Edit under Table.

   ![ADF Pencil.](./media/exercise_7_add_connections_edit_table.png 'ADF IR Connection Icon') 
   
4.	Add the Dynamic Content for Schema name.

   ![ADF Pencil.](./media/exercise_7_add_dynamic_content.png 'ADF IR Connection Icon') 
    
5.	Select the schemaname parameter created, Click Finish.

   ![ADF Pencil.](./media/exercise_7_add_schemaname_parameter.png 'ADF IR Connection Icon') 
   
6. Similarly Add dynamic content for table name.
   
7.	Select the tablename parameter created, Click Finish.

   ![ADF Pencil.](./media/exercise_7_add_tablename_parameter.png 'ADF IR Connection Icon') 
   
8. Click on Validate All and Publish All at the top to validate and save the changes.
   
   
## Exercise 8: Azure Data Factory - Linked Services for Azure Blob for backup

Create Linked Service to connect to Azure Blob.

1.	Click on Connections -> Linked Services -> New.

2.	From Azure,  Click on Azure Blob Storage.

   ![ADF Pencil.](./media/exercise_8_blob_Storage.png 'ADF IR Connection Icon') 
   
3.	Set up the configuration details.

   a. Enter the name as bctlbackup.
   
   b. Account Selection method as From Azure Subscription.
   
   c. Azure Subscription – Select the one used for this lab.
   
   d. Storage Account name as the one created during before HOL.
   
   e. Click on Test Connection and then Create.

   ![ADF Pencil.](./media/exercise_8_enter_details.png 'ADF IR Connection Icon')
   
## Exercise 9: Azure Data Factory - Dataset for Azure Blob

1.	Click on Datasets (…) and select New Dataset.

2.	From Azure,  Click on Azure Blob Storage.

3.	Choose the Format as Delimited Text CSV.

4.	Set up the configuration.

   a.	Enter the name as bctlbackupdataset.
   b.	Select the Linked Service as bctlbackup.
   c.	File path: Click on Browse and select the container created during before HOL.
   d.	Check First Row as Header.
   e. Import Schema: From connection/store.
   f.	Click OK.

   ![ADF Pencil.](./media/exercise_9_enter_details.png 'ADF IR Connection Icon')

## Exercise 10: Azure Data Factory - Adding Parameters to bctlbackupdataset 

Since this is a common connection to Azure Blob, we can dynamically pass the container name.

1.	Click on Parameters and add two parameters.

   ![ADF Pencil.](./media/exercise_10_add_parameters.png 'ADF IR Connection Icon') 
   
2.	Click on Connections tab, click on Add Dynamic Content under Directory.

   ![ADF Pencil.](./media/exercise_10_add_dynamic_content.png 'ADF IR Connection Icon') 
   
3.	Select the directoryname parameter created and Click Finish.

   ![ADF Pencil.](./media/exercise_10_add_foldername_parameters.png 'ADF IR Connection Icon') 
   
4.	Select the Column Delimiter as tab.

   ![ADF Pencil.](./media/exercise_10_column_delimiter.png 'ADF IR Connection Icon') 
   
5. Click on Validate All and Publish All at the top to validate and save the changes	e.	Click on Validate All and Publish All at the top to validate and save the changes.

## Exercise 11: Azure Data Factory - Create Pipeline 

1.	Connect to Current Process Folder.
2.	Get Current files count, if not <> 1 send email notification.
3.	If Current Process file is one, 
   a.	Load the Current Process file into Sql Server, send email on number of records loaded.
   b.	Take a backup in Azure Blob.
   c.	Delete the File from Local Folder.
4.	Check If day of month < 9.
   a.	Connect to Previous Process Folder.
   b.	Get Previous files count, if not <> 1 send email notification.
   c.	If Previous Process file count is one, 
   d.	Load both Current Process file & Previous Process File into Sql Server, send email on number of records loaded.
   e.	Take backups in Azure Blob.
   f.	Delete the Files from Local Folder.

## Exercise 12: Azure Data Factory - Create Generic Pipeline 

Create a Generic Pipeline to perform on the following which can be called for both Current and Previous files.

1. Load the Process file into Sql Server
2. Send email on number of records loaded.
3.	Take a backup in Azure Blob.
4.	Delete the File from Local Folder.

We will start with creating a new pipeline.

1.	Click on Pipeline(…) and select New Pipeline.

   ![ADF Pencil.](./media/exercise_12_new_pipeline.png 'ADF IR Connection Icon')  
   
2.	Enter the name as generic_copy_pipeline.

   ![ADF Pencil.](./media/exercise_12_name_pipeline.png 'ADF IR Connection Icon')  
   
3.	Click on Parameters to add parameters foldername, filename, schemaname, tablename, precopyscript which will be referenced in Datasets created above.

   ![ADF Pencil.](./media/exercise_12_parameter_pipeline.png 'ADF IR Connection Icon')  
   
## Task 1 : Add Copy Activity to copy into Sql Server

1. From Activities pane, expand Move &Transform to drag and drop the Copy Activity, name the activity as CopyCurrentProcess.

   ![ADF Pencil.](./media/exercise_12_task1_add_copy_activity.png 'ADF IR Connection Icon')  

2. Click on Source tab and select SourceProcessFile as Dataset and provide the value for foldername parameter as @pipeline().parameters.foldername and filename as single blank.

   ![ADF Pencil.](./media/exercise_12_task1_add_source_parameters.png 'ADF IR Connection Icon')  

3. Click on Sink tab and select OutputSqltable as Dataset and provide the value for tablename as etl_demo_raw and schema name as dbo. Check Auto Create table. Give Pre-Copy Script as below to delete the existing records and load fresh records in case of first activity call.

   ![ADF Pencil.](./media/exercise_12_task1_add_sink_parameters.png 'ADF IR Connection Icon') 
   
4. Click Validate All and Publish All to validate and save the changes.
   
## Task 2 : Add Copy Activity to take backup in Blob

1. Add one more Copy activity, name it as CopyBackuptoBlob and connect Success Output of CopyCurrentProcess to CopyBackuptoBlob activity.

   ![ADF Pencil.](./media/exercise_12_task2_add_copy_activity.png 'ADF IR Connection Icon')  
   
2. Click on Source and select SourceProcessFile and pass the value for parameter as @pipeline().parameters.foldername and filename as one blank.

   ![ADF Pencil.](./media/exercise_12_task2_add_source_parameters.png 'ADF IR Connection Icon')  
   
3. Click on Sink and select bctlbackupdataset. Enter the parameter value as @pipeline().parameters.foldername.

   ![ADF Pencil.](./media/exercise_12_task2_add_sink_parameters.png 'ADF IR Connection Icon')  
   
4. Click on Validate All and Publish All.

## Task 3 : Add Delete Activity to Delete File from Local

1. Add Delete Activity next to CopyBackuptoBlob and name the activity as DeleteFilefromLocal.

   ![ADF Pencil.](./media/exercise_12_task3_delete_activity.png 'ADF IR Connection Icon')  
   
2. Click on Source and select SourceProcessFolder and add dynamic content to foldername as @pipeline().parameters.foldername, add dynamic content to filename as @pipeline().parameters.filename.

   ![ADF Pencil.](./media/exercise_12_task3_add_source_parameters.png 'ADF IR Connection Icon')  
   
3. Click on Logging Settings and disable logging for this demo.

   ![ADF Pencil.](./media/exercise_12_task3_add_logging_parameters.png 'ADF IR Connection Icon')  
   
4. Click on Validate All and Publish All.


## Task 4 : Add Web Activity to call Logic Apps Email

1. From Activity expand General, Add Web activity next to CopyCurrentProcess to call the Logic App to send email notification on number of records loaded, name the activity as EmailRecordsLoaded. Connect Success Output of CopyCurrentProcess to EmailRecordsLoaded.

   ![ADF Pencil.](./media/exercise_12_task4_add_web_activity.png 'ADF IR Connection Icon')  
   
2. Click on Settings.

   a. Copy Paste the Logic App http URL.
   
   b. Select API method as POST.
   
   c. Add Headers with name as Content-Type  and value as application/json. 

   d. Add Dynamic Content to Body
{"DataFactoryName":"@{pipeline().DataFactory}","EmailTo":"replacewithyourid","Message":"@{pipeline().parameters.foldername}  File Copied Successfully. \n No of records copied - @{string(activity('CopyCurrentProcess').output.rowsCopied)}","PipelineName":"@{pipeline().Pipeline}","Subject":"Data Copy from FTP to SqlServer - Success"}.

   ![ADF Pencil.](./media/exercise_12_task4_add_settings_parameters.png 'ADF IR Connection Icon')  
   
3. Click on Validate All and Publish All.

## After the hands-on lab

Duration: 10 minutes

In this exercise, attendees will deprovision any Azure resources that were created in support of the lab.

### Task 1: Delete resource group

1. Using the Azure portal, navigate to the Resource group you used throughout this hands-on lab by selecting **Resource groups** in the menu.

2. Search for the name of your research group and select it from the list.

3. Select **Delete** in the command bar and confirm the deletion by re-typing the Resource group name and selecting **Delete**.

You should follow all steps provided _after_ attending the Hands-on lab.
