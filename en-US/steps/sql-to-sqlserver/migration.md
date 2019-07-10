## Migration overview

After you have the necessary prerequisites in place and have completed the tasks associated with the **Pre-migration** stage, you are ready to perform the schema and data migration.

## Migrate schema and data

After assessing your databases, the next step is to begin the process of migrating the schema and database by using DMA.

### Steps

To use DMA to create a migration project, perform the following steps.

1. Create a **New Migration** project

    a. Select the New icon, select the **Migration** project type, select **SQL Server** as source and target types, and then select **Create**.

    ![New Migration](https://mpbdevcontent.azureedge.net/Images/scenario-assets/dmamigrate.png)    

    b. Provide source and target SQL server connection details, and then select **Next**.

    ![Source & Target details](https://mpbdevcontent.azureedge.net/Images/scenario-assets/dmasourcetarget.png)    

    c. Select databases from the source to migrate, and then specify the **Shared location accessible by source and target SQL servers for backup operation**. 
     
    Note: Be sure that the service account running the source SQL Server instance has write privileges on the shared location and that the target SQL Server service account has read privileges on the shared location.

    ![Select databases to migrate](https://mpbdevcontent.azureedge.net/Images/scenario-assets/dmamigrateadddb.png) 

    d. Select **Next**, select the logins that you want to migrate, and then select **Start Migration**.

    ![Migration Logins](https://mpbdevcontent.azureedge.net/Images/scenario-assets/dmaselectlogins.png) 

    e. Now, monitor the progress of migration in the **View Results** screen.

    ![Migration View Results](https://mpbdevcontent.azureedge.net/Images/scenario-assets/dmamigrateresults.png) 
  
2. **Review Migration Results**

    a. Select **Export report** to save the migration results to a .csv or .json file.

    b. Review the saved file for details about data and logins migration and verify successful completion of the process.

## Data sync and Cutover

For minimal-downtime migrations, the source you are migrating continues to change after the one-time migration occurs, and it will drift from the target in terms of data and schema. During this phase, you need to ensure that all changes in the source are captured and applied to the target in near real time. After you verify that all changes in source have been applied to the target, you can cutover from the source to the target environment.

Support for minimal-downtime migrations is not yet available for this scenario, so the Data sync and Cutover phases are not currently applicable.
