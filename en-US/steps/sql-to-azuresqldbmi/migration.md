## Migration overview

After you have the necessary prerequisites in place and have completed the tasks associated with the **Pre-migration** stage, you are ready to perform the schema and data migration.

## Migrate schema and data

After assessing your databases, the next step is to execute the schema migration process. With the Azure Database Migration Service, schema migration takes place as part of the broader migration process.

**Important**: If you use SQL Server Integration Services (SSIS), DMS does not currently support migrating the catalog database for your SSIS projects/packages (SSISDB) from SQL Server to Azure SQL Database Managed Instance. However, you can provision SSIS in Azure Data Factory (ADF) and redeploy your SSIS projects/packages to the destination SSISDB hosted by Azure SQL Database Managed Instance. For more information about migrating SSIS packages, see the article [Migrate SQL Server Integration Services packages to Azure](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages).

### Overview of schema and data migration steps

An overview of the steps associated with using Azure DMS to migrate the schema and data follows.

1.	Register the Microsoft.DataMigration resource provider.
2.	Create an Azure Database Migration Service instance.
3.	Create a migration project.
4.	Specify source details.
5.	Specify target details.
6.	Select source databases.
7.	Configure migration settings.
8.	Review the migration summary.
9.	Run and monitor the migration.

**Important**: For detail on the specific steps associated with:
* Online migrations, see the information [here](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online#register-the-microsoftdatamigration-resource-provider).
* Offline migrations, see the information [here](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance#register-the-microsoftdatamigration-resource-provider).

## Data sync and Cutover

With minimal-downtime migrations, the source you are migrating continues to change, drifting from the target in terms of data and schema, after the one-time migration occurs. During the **Data sync** phase, you need to ensure that all changes in the source are captured and applied to the target in near real time. After you verify that all changes in source have been applied to the target, you can cutover from the source to the target environment.

**Important**: For detail on the specific steps associated with performing a cutover as part of online migrations, see the information [here](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online#performing-migration-cutover).
