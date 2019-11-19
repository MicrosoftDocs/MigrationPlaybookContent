## Pre-migration overview

After verifying that your source environment is supported and ensuring that you have addressed any prerequisites, you are ready to start the Pre-migration stage. This part of the process involves conducting an inventory of the databases that you need to migrate, assessing those databases for potential migration issues or blockers, and then resolving any items you might have uncovered. For heterogenous migrations (such as Oracle to Azure Database for PostgreSQL), this stage also involves converting the schema(s) in the source database(s) to be compatible with the target environment. For homogenous migrations, such as SQL Server to SQL on Azure VMs, conversion of the source schema to work in the target environment is not required.

## Discover

The goal of the Discover phase is to identify existing data sources and details about the features that are being used to get a better understanding of and plan for the migration. This process involves scanning the network to identify all your organization’s SQL instances together with the version and features in use.

To use the MAP Toolkit to perform an inventory scan, perform the following steps.

### Steps

1. Run the MAP Toolkit.

    a. Open the MAP Toolkit, and then on the left pane, select **Database**.
    
    You will be on the following screen:
    
    ![MAP Overview](https://mpbdevcontent.azureedge.net/Images/scenario-assets/_shared/mapoverview.png)
    
    b. Select **Create/Select database**.
    
    ![MAP Create/Select DB](https://mpbdevcontent.azureedge.net/Images/scenario-assets/_shared/mapselectdb.png)
     
    c. Ensure that **Create an inventory database** is selected, enter a name for the database, a brief description, and then select **OK**.
    
    ![MAP Create/Select DB Overview](https://mpbdevcontent.azureedge.net/Images/scenario-assets/_shared/mapselectdboverview.png)
    
    The next step is to collect data from the database created.

    d. Select **Collect inventory data**.
    
    ![MAP Collect Inventory Data](https://mpbdevcontent.azureedge.net/Images/scenario-assets/sql-to-sqlvm/mapcollectinventorydata.png)
    
    e. In the Inventory and Assessment Wizard, select **SQL Server** and **SQL Server with Database Details**, and then select **Next**.
    
    ![MAP Inventory and Assessment Wizard](https://mpbdevcontent.azureedge.net/Images/scenario-assets/sql-to-sqlvm/mapinventorywizard.png)
    
    f. Select the best method option to search the computers on which Microsoft Products are hosted, and then select **Next**.
    
    ![MAP Inventory and Assessment Wizard Discovery Methods](https://mpbdevcontent.azureedge.net/Images/scenario-assets/_shared/mapdiscoverymethods.png)
    
    g. Enter credentials or create new credentials for the systems that you want to explore, and then select **Next**.
    
   ![MAP Inventory and Assessment Wizard Discovery Credentials](https://mpbdevcontent.azureedge.net/Images/scenario-assets/_shared/mapdiscoverycreds.png)
    
    h. Set the order of the credentials, and then select **Next**.
               
    ![MAP Inventory and Assessment Wizard Discovery Credentials Order](https://mpbdevcontent.azureedge.net/Images/scenario-assets/sql-to-sqlvm/mapdiscoverycredsorder.png)
    
    Now, you need to specify the credentials for each computer that you want to discover. You can use unique credentials for each computer/machine, or you can choose to use the **All Computer Credentials** list.
    
    i. After setting up the credentials, select **Save**, and then select **Next**.
    
    ![MAP Inventory and Assessment Wizard Discovery Credentials](https://mpbdevcontent.azureedge.net/Images/scenario-assets/_shared/mapdiscoverycredsindividual.png)
    
    j. Verify your selection summary, and then select **Finish**.
    
    ![MAP Inventory and Assessment Wizard Summary](https://mpbdevcontent.azureedge.net/Images/scenario-assets/_shared/mapdiscoverysummary.png)
    
    k. Wait for a few minutes (depending on the number of databases) for the Data Collection summary report.
    
    ![MAP Inventory and Assessment Wizard Summary](https://mpbdevcontent.azureedge.net/Images/scenario-assets/_shared/mapdatacollectionsummary.png)
    
    l. Select **Close**.
    
    The Main window of the tool appears, showing a summary of the Database Discovery completed so far.
    
 2. Generate a report.
    
    On the top-right corner of the tool, an **Options** page appears, which you can use to generate report about the SQL Server Assessment and the Database Details.
    
    ![MAP Report Generation](https://mpbdevcontent.azureedge.net/Images/scenario-assets/sql-to-sqlvm/mapexcelreport.png)
    
    a. Select both options (one by one) to generate the report.
    
    This will take a couple of seconds to a few minutes depending on the size of the inventory completed during discovery.
    
    ![MAP Report Generation](https://mpbdevcontent.azureedge.net/Images/scenario-assets/_shared/mapexcelreportdone.png)

## Assess

After identifying the data sources, the next step is to assess the on-premises SQL Server instance(s) migrating to a specific version of SQL Server on Azure VMs so that you understand the gaps between the source and target instances. Use the Data Migration Assistant (DMA) to assess your source database before migrating your SQL Server instance.

### Steps

To use DMA to create an assessment, perform the following steps.

1. Create a new assessment project.

    a. Launch DMA, select the New (+) icon, select the **Assessment** project type, specify a project name, select **SQL Server** as the source and target, and then select **Create**.
    
    ![New Assessment](https://mpbdevcontent.azureedge.net/Images/scenario-assets/sql-to-sqlvm/dmanewproject.bmp)    
    
    b. Select the target SQL Server version that you plan to migrate to and against which you need to run an assessment, select one or both of the assessment report types (**Compatibility Issues** and **New features’ recommendation**), and then select **Next**.
    
    ![Report Types](https://mpbdevcontent.azureedge.net/Images/scenario-assets/sql-to-sqlvm/dmaassessment.bmp)   
    
    c. In the **Connect to a server** fly-out, specify the name of the SQL Server instance to connect to, specify the Authentication type and Connection properties, and then select **Connect**.
    
    d. In the **Add Sources** fly-out, select the database(s) you that want to assess, and then select **Add**.
            
    ![Add databases](https://mpbdevcontent.azureedge.net/Images/scenario-assets/sql-to-sqlvm/dmaadddb.bmp)   
    
    e. Select **Start Assessment**.
    
    Now wait for the assessment results; the duration of the assessment depends on the number of databases added and the schema size of each database. Results will be displayed per database as soon as they are available.
    
    f. Select the database that has completed assessment, and then switch between **Compatibility issues** and **Feature recommendations** by using the switcher.
    
    ![Assessment results](https://mpbdevcontent.azureedge.net/Images/scenario-assets/sql-to-sqlvm/dmaassessmentresults.bmp)  
    
    g. Review the compatibility issues by analyzing the impacted object and its details for every issue identified under **Breaking changes**, **Behavior changes**, and **Deprecated features**.
    
    h. Review feature recommendations across the **Performance**, **Storage**, and **Security** areas.
    
    Feature recommendations cover a variety of features such as In-Memory OLTP and Columnstore, Stretch Database, Always Encrypted (AE), Dynamic Data Masking (DDM), and Transparent Data Encryption (TDE). 
    
2. Review the assessment results.

    a. After all database assessments are complete, select **Export report** to export the results to either a JSON or CSV file for analyzing the data at your own convenience.

## Convert

After assessing the source database instance(s) you are migrating, for heterogenous migrations, you need to convert the schema to work in the target environment. Since this is a homogeneous migration, the Convert phase is unnecessary.
