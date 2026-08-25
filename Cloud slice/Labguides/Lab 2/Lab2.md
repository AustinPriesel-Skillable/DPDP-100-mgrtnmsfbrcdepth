<!--
lab:
  title: 'Lab 2: Migrate Azure Synapse Analytics SQL objects to Fabric Data Warehouse'
  description: In this lab, you successfully migrated data from Azure Synapse Analytics to Microsoft Fabric Data Warehouse. You created a new warehouse, configured a pipeline with a Synapse SQL source, and loaded data into Fabric using OneLake. After executing the pipeline, you validated the data by comparing row counts between Synapse and Fabric. Finally, you scheduled the pipeline to automate recurring data transfers, ensuring a streamlined and scalable migration process.
  duration: 96 minutes
  level: 300
  islab: true
  primarytopics:
    - Azure
    - Azure Synapse Analytics
    - Microsoft Fabric
-->

## **Lab 2: Migrate Azure Synapse Analytics SQL objects to Fabric Data Warehouse**

### Introduction

This lab focuses on migrating SQL objects and data from **Azure Synapse Analytics (Dedicated SQL Pool)** to **Microsoft Fabric Data Warehouse**. It demonstrates how to create a warehouse in Fabric, establish a connection to Synapse, and use pipelines to copy data into OneLake. The lab also covers validating migrated data and scheduling pipelines for automated data movement.

### Objective

By the end of this lab, you will be able to:

- Create a **Data Warehouse** in Microsoft Fabric

- Establish a **linked connection** to Azure Synapse SQL

- Build and execute a **data pipeline** to copy data from Synapse to Fabric

- Load data into **Fabric Warehouse tables** using Copy Data activity

- Validate data migration using **SQL queries**

- Schedule pipelines for **automated execution**

## Task 1: Create a Warehouse

1. Open your browser, navigate to the address bar, and type or paste the following URL: +++https://app.fabric.microsoft.com/+++ then press the **Enter** button.

1. Create a new Warehouse by clicking on the **+New item** button in the navigation bar.

1. Click on the "**Warehouse**" tile.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image1.png)

1. In the **New warehouse** dialog box, enter **+++sqlpoolmigrate+++** in the **Name** field, click on the **Create** button and open the new warehouse.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image2.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image3.png)

1. Click on **Fabric_migration@lab.LabInstance.Id** workspace in the left-sided navigation bar  

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image4.png)

## Task 2: Create Linked Connection to Synapse SQL

1. In the **Fabric_migration@lab.LabInstance.Id** page, select +**New item**. Then, click **Pipeline** to view the full list of available items under Get data.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image5.png)

1. On the **New** **pipeline** dialog box, in the **Name** field, enter +++sqlpool_migratepipeline+++ and click on the **Create** button.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image6.png)

1. On newly created pipeline, select **Copy data** dropdown and choose **Add copy data activity** option.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image7.png)

1. With the **copy data** being selected, navigate to **Source** tab.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image8.png)

1. Select the **Connection** dropdown and select **Browse all** option.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image9.png)

1. Select **+ New** from the left pane  

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image10.png)

1. From the data source options, select **Azure Synapse Analytics (SQL DW)** to begin the connection setup.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image11.png)

1. Select **New Connection → Azure Synapse Analytics (SQL)**

1. Enter details:

    - **Server name:** *{your-synapse-sql-endpoint}*.sql.azuresynapse.net

    - **Database:** your dedicated sql pool

    - **Authentication:** Basic

    - **Usename:** +++sqladmin+++

    - **Password:** +++password321!+++

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image12.png)

1. Open the **Table** dropdown and select the **fabric_employee** table.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image13.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image14.png)

1. Now, navigate to **destination** tab.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image15.png)

1. Click **Destination** tab

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image16.png)

1. On choose a destination window, select **OneLake catalog** from the left pane and select the **sqlpoolmigrate**.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image17.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image18.png)

1. Under the Destination tab, select the **Auto create** *table* option and specify the table as +++dbo.employee+++ for the data load.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image19.png)

1. Click on **Run** to run the copy data.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image20.png)

1. Click on **Save and run** button so that pipeline will be save and run.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image21.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image22.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image23.png)

1. After the successful execution of the pipeline, go to your SQL analytics endpoint Lakehouse and open the explorer to see the imported data.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image24.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image25.png)

1. Select **New SQL query** to write your SQL statements.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image26.png)

1. Paste the code as shown in the image below, then click the **Play** icon to run it and observe the counts in the output.

    `SELECT COUNT(*) FROM dbo.employee;`

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image27.png)

    `SELECT TOP 10 \* FROM dbo.employee;`

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image28.png)

1. Compare row counts with Synapse: go back to the Synapse workspace, navigate to **Develop**, and select **SQL script**.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image29.png)

1. Ensure that the SQL script is connected to the **SQL dedicated pool** by selecting it from both the ‘Connect to’ dropdown and the ‘Use database’ dropdown, as highlighted in the image

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image30.png)

1. Enter the following code into the editor and click **Run** to execute it

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image31.png)

    `SELECT TOP 10 * FROM dbo.employee;`

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image32.png)

## Task 3: Schedule the Pipeline

1. Now, click on **Fabric_migration@lab.LabInstance.Id** on the left-sided navigation pane and select **sql_migratepipeline**

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image33.png)

1. Click **Schedule**

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image34.png)

1. Select **+ Add schedule** and configure the schedule as required then select **Save** and close the **Schedule** panel.

    >[!Note] The example here schedules the pipeline to execute daily at  8:00 PM until the end of the year.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image35.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image36.png)

## Task 4: Delete the Resources

1. To delete resources , type **Resource groups** in the Azure portal search bar, navigate and click on **Resource groups** under **Services**.

    ![A screenshot of a computer Description automatically generated](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image37.png)

1. In the Resource groups page, select your resource group.

1. On the **Resource Group** home page, select all resources and then click **Delete**.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image38.png)

1. In the **Delete Resources** pane that appears on the right side, navigate to **Enter “delete” to confirm deletion** field, then click on the **Delete** button

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image39.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image40.png)

1. Go to your +++https://app.fabric.microsoft.com/+++ Microsoft Fabric workspace

1. Select the **...** option under the workspace name and select **Workspace settings**.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image41.png)

1. Select **General** and **Remove this workspace.**

    ![A screenshot of a computer AI-generated content may be
    incorrect.](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image42.png)

1. Click on **Delete** in the warning that pops up.

    ![](https://raw.githubusercontent.com/technofocus-pte/mgrtnmsfbrcdepth/refs/heads/main/Cloud%20slice/Labguides/Lab%202/media/image43.png)

### Summary

In this lab, you successfully migrated data from Azure Synapse Analytics to Microsoft Fabric Data Warehouse. You created a new warehouse, configured a pipeline with a Synapse SQL source, and loaded data into Fabric using OneLake. After executing the pipeline, you validated the data by comparing row counts between Synapse and Fabric. Finally, you scheduled the pipeline to automate recurring data transfers, ensuring a streamlined and scalable migration process.
