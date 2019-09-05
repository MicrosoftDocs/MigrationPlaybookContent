## Migration overview

After you have the necessary prerequisites in place and have completed the tasks associated with the **Pre-migration** stage, you are ready to perform the schema and data migration.

## Migrate schema

After you are comfortable with the assessment and satisfied that the selected database is a viable candidate for migration to Azure SQL Database, use the Data Migration Assistant (DMA) to migrate the schema to Azure SQL Database.

**Note**: Before you create a migration project in DMA, be sure that you have already provisioned an Azure SQL database as mentioned in the prerequisites.

### Overview of schema migration steps

An overview of the steps associated with using DMA to migrate the schema follows.

1. Open DMA, and then begin creating a new migration project.
2. Specify a project name, select SQL Server as the source server type, and then select Azure SQL Database as the target server type.
3. Specify the migration scope as Schema only, and then create the project.
4. Specify the source connection details for your SQL Server, and then connect to the source database.
5. Specify the target connection details for the Azure SQL database, and then connect to the database you had pre-provisioned in Azure SQL Database.
6. Specify the schema objects in the source database that need to be deployed to Azure SQL Database.
7. Generate SQL scripts, and then review them for any errors.
9. Fix the objects that report errors by leveraging the recommendations provided by your DMA assessment.
8. Deploy the schema to Azure SQL Database, and then check the target server for any anomalies.

**Important**: For detail on the specific steps associated with:

* Online migrations, see the information in [Migrate SQL Server to a single database or pooled database in Azure SQL Database online using DMS](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online#migrate-the-sample-schema).
* Offline migrations, see the information in [Migrate SQL Server to a single database or pooled database in Azure SQL Database offline using DMS](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql#migrate-the-sample-schema).

## Migrate data

When your schema has been successfully migrated to the target, the next step is to execute the data movement by using the Azure Database Migration Service (DMS).

**Note**: You can also use DMA to migrate databases. However, DMA is best for performing proofs of concept (PoCs), test database migrations, or for relatively small database migration efforts. Note that when using DMA for data migration, you can only move one database at a time. For more information, see the article [Migrate on-premises SQL Server using Data Migration Assistant](https://docs.microsoft.com/en-us/sql/dma/dma-migrateonpremsql).
 
### Overview of data migration steps

An overview of the steps associated with using Azure DMS to migrate the data follows.

1. Register the Microsoft.DataMigration resource provider.
2. Create an instance of DMS.
3. Create a migration project in DMS.
4. Specify source details for the migration.
5. Specify target details for the migration.
6. Run the migration.
7. Monitor the migration.

**Important**: For detail on the specific steps associated with:

* Online migrations, see the information in [Migrate SQL Server to a single database or pooled database in Azure SQL Database online using DMS](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online#register-the-microsoftdatamigration-resource-provider).
* Offline migrations, see the information in [Migrate SQL Server to a single database or pooled database in Azure SQL Database offline using DMS](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql#register-the-microsoftdatamigration-resource-provider).

## Data sync and Cutover

With minimal-downtime migrations, the source you are migrating continues to change, drifting from the target in terms of data and schema, after the one-time migration occurs. During the **Data sync** phase, you need to ensure that all changes in the source are captured and applied to the target in near real time. After you verify that all changes in source have been applied to the target, you can cutover from the source to the target environment.

**Important**: For detail on the specific steps associated with performing a cutover as part of online migrations, see the information in [Migrate SQL Server to a single database or pooled database in Azure SQL Database online using DMS](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online#perform-migration-cutover).
