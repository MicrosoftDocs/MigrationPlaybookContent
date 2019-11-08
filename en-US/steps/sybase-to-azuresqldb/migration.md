## Migration overview

After you have the necessary prerequisites in place and have completed the tasks associated with the **Pre-migration** stage, you are ready to perform the schema and data migration.

## Migrate schema and data

### Overview

After you have completed assessing your databases and addressing any discrepancies, the next step is to execute the migration process. Migration involves two steps – publishing the schema and migrating the data. SSMA for Sybase is the correct tool to use for this process.

### Steps

To use SSMA for Sybase to publish the database schema and migrate the data, perform the following steps.

1. Setting migration options

    _Review the project migration otpions in the Project Settings dialog._

2. Migrate data to SQL Server.

    _After the migration is complete you will be able to view the migration report._

**Note**: For complete step-by-step guidance on publishing the schema and migrating the data, see the following resource:

* The article [Migrating Sybase ASE Databases to SQL Server - Azure SQL DB (SybaseToSql)](https://docs.microsoft.com/en-us/sql/ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql).
* The blog posting [SQL Server Migration Assistant: How to assess and migrate data from non-Microsoft data platforms to SQL Server](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/).

## Data sync and Cutover

With minimal-downtime migrations, the source you are migrating continues to change, drifting from the target in terms of data and schema, after the one-time migration occurs. During the **Data sync** phase, you need to ensure that all changes in the source are captured and applied to the target in near real time. After you verify that all changes in source have been applied to the target, you can cutover from the source to the target environment.

The Azure Database Migration Service does not yet support minimal-downtime migrations for this scenario, so the **Data sync** and **Cutover** phases are not currently applicable.
