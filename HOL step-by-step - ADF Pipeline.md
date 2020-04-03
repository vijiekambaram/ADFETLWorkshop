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
   
b. Click on Integration runtimes and then +New.

   ![ADF Pencil.] (./media/exercise_1_IR_Click.png 'ADF IR Connection Icon') 
   
c. Click on Azure, Self-Hosted -> Continue.

   ![ADF Pencil.] (./media/exercise_1_azure_self_hosted.png 'ADF IR Connection Icon')
 
d. Select Self Hosted and then Continue.

   ![ADF Pencil.] (./media/exercise_1_setup_self_hosted.png 'ADF IR Connection Icon')
   
e. Enter the details as below i.e Name as SelfHostedForLocal and Description as To Connect to Local and click on Create.

   ![ADF Pencil.] (./media/exercise_1_IR_enter_details.png 'ADF IR Connection Icon')

f.	Click on Option 1 for express set up.

   ![ADF Pencil.] (./media/exercise_1_express_setup.png 'ADF IR Connection Icon')
   
g.	Click on the Link in Option1 to download the integration run time. Copy and paste the authentication key in case of Option2.

h.	Download the self-hosted integration runtime on a local Windows machine. Run the installer. It will take few minutes for set up.

   ![ADF Pencil.] (./media/exercise_1_run_express_setup.png 'ADF IR Connection Icon')
   
i.	Once it is done, it gets listed under Nodes tab of the IR.

   ![ADF Pencil.] (./media/exercise_1_node_ready.png 'ADF IR Connection Icon')
   

## Exercise 2: Azure Data Factory - Linked Services for Local Folder

This exercise is to create connections to connect to Local folder.

1.	Create Linked Service to connect to Local Folder.

2.	Click on Connections -> Linked Services -> New.

3.	Click on File and select File System.

   ![ADF Pencil.] (./media/exercise_2_ls_select_fs.png 'ADF IR Connection Icon')

4.	Download the BCTL Zip files sent via email into Local folder. Copy the path of Local Folder as follows.

   ![ADF Pencil.] (./media/exercise_2_local_folder_structure.png 'ADF IR Connection Icon')
   
5.	Enter the name as LocalFileServer, IR as SelfHostedForLocal, Host as your local directory that is copied in previous step i.e, Username as your DOMAIN\Windows login, Password as Windows login Password. Click on Test Connection and then Create.

   ![ADF Pencil.] (./media/exercise_2_ls_enter_details.png 'ADF IR Connection Icon')


## Exercise 3: Azure Data Factory - Dataset for Local Folder

Dataset is use to define the folder name, file type etc.

1. Click on Datasets (…) and select New Dataset.

   ![ADF Pencil.] (./media/exercise_3_create_new_dataset.png 'ADF IR Connection Icon')
   
2.  Click on File, Select File System. Click Continue.

   ![ADF Pencil.] (./media/exercise_3_ds_select_fs.png 'ADF IR Connection Icon')
   
   
3. 


## After the hands-on lab

Duration: 10 minutes

In this exercise, attendees will deprovision any Azure resources that were created in support of the lab.

### Task 1: Delete resource group

1. Using the Azure portal, navigate to the Resource group you used throughout this hands-on lab by selecting **Resource groups** in the menu.

2. Search for the name of your research group and select it from the list.

3. Select **Delete** in the command bar and confirm the deletion by re-typing the Resource group name and selecting **Delete**.

You should follow all steps provided _after_ attending the Hands-on lab.
