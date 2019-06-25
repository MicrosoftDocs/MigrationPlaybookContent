## Migration overview

After you have the necessary prerequisites in place and have completed the tasks associated with the **Pre-migration** phase, you are ready to perform the actual migration.

There are several methods for migrating a SQL Server database to an instance of SQL Server on Azure Virtual Machines (Azure VMs).

### Overview of migration methods

The list below identifies the primary methods for migrating from SQL Server to SQL Server on Azure VMs.
* Use the Data Migration Assistant (DMA) to migrate the schema and data into an Azure VM.
* Perform an on-premises backup using compression, and then manually copy the backup file into an Azure VM.
* Perform a backup to URL, and then restore into an Azure VM from the URL.
* Detach and copy the data and log files to Azure Blob storage, and then attach to an Azure VM from the URL.
* Convert an on-premises VM to Hyper-V VHDs, upload to Azure Blob storage, and then deploy a new Azure VM using the uploaded VHD.
* Ship a hard drive using Windows Import/Export Service.
* Use the Add Azure Replica Wizard.
* Use SQL Server transactional replication.

A couple of key points to consider when reviewing the migration methods to determine the best option for your business scenario:
* For optimum data transfer performance, migrate database files into the SQL Server on Azure VM instance using a compressed backup file.
* To minimize downtime during the database migration process, use either the AlwaysOn option or the transactional replication option.

**Tip**: There is no supported way to upgrade the version/edition of an existing SQL Server on Azure VM instance. Instead, create a new SQL Server on Azure VM instance running the desired version/edition, and then use one of the techniques in the table above to move your databases.

If it is not possible to use the above methods, migrate your database manually. Using this method, you will generally start with a database backup followed by a copy of the database backup into Azure and then perform a database restore. You can also copy the database files themselves into Azure and then attach them.

**Note**: When upgrading from older versions of SQL Server to SQL Server 2014 or SQL Server 2016, we recommend that you address all dependencies on features that are not supported by the later version of SQL Server as part of the migration project. For more information on the supported editions and scenarios, see the article [Upgrade SQL Server](https://msdn.microsoft.com/library/bb677622.aspx).

The following section provides details about using DMA to migrate the schema and data to an Azure VM.

For additional information about the other options for migrating from SQL Server on-premises to SQL Server on Azure VMs, see the article [Migrate a SQL Server database to SQL Server in an Azure VM](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql).

## Migrate schema and data

After assessing your databases, the next step is to begin the process of migrating the schema and database by using DMA.

### Steps

To use DMA to create a migration project, perform the following steps.

1. Create a **New Migration** project

    a. Select the New icon, select the **Migration** project type, select **SQL Server** as source and target types, and then select **Create**.

    ![New Migration](https://mpbdevcontent.azureedge.net/Images/dmamigrate.png)    

    b. Provide source and target SQL server conenction details, and then select **Next**.

    ![Source & Target details](https://mpbdevcontent.azureedge.net/Images/dmasourcetarget.png)    

    c. Select databases from the source to migrate, and then specify the **Shared location accessible by source and target SQL servers for backup operation**. 
     
    **Note**: Be sure that the service account running the source SQL Server instance has write privileges on the shared location and that the target SQL Server service account has read privileges on the shared location.

    ![Select databases to migrate](https://mpbdevcontent.azureedge.net/Images/dmamigrateadddb.png) 

    d. Select **Next**, select the logins that you want to migrate, and then select **Start Migration**.

    ![Migration Logins](https://mpbdevcontent.azureedge.net/Images/dmaselectlogins.png) 

    e. Now, monitor the progress of migration in the **View Results** screen.

    ![Migration View Results](https://mpbdevcontent.azureedge.net/Images/dmamigrateresults.png) 
  
2. **Review Migration Results**

    a. Select **Export report** to save the migration results to a .csv or .json file.

    b. Review the saved file for details about data and logins migration and verify successful completion of the process.

**Note**: If you are interested in participating in a Private preview of a one-time migration for SQL Server to Azure SQL Database using the Azure Database Migration Service, submit a nomination on the Azure Database Migration Service [Preview page](https://aka.ms/dms-preview).

## Data sync and Cutover

For minimal-downtime migrations, the source you are migrating continues to change after the one-time migration occurs, and it will drift from the target in terms of data and schema. During this phase, you need to ensure that all changes in the source are captured and applied to the target in near real time. After you verify that all changes in source have been applied to the target, you can cutover from the source to the target environment.

Support for minimal-downtime migrations is not yet available for this scenario, so the Data sync and Cutover phases are not currently applicable.