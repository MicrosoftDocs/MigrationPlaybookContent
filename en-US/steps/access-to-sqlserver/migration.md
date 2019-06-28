## Migration overview

After you have the necessary prerequisites in place and have completed the tasks associated with the **Pre-migration** stage, you are ready to perform the schema and data migration.

## Migrate

After you have completed assessing your databases and addressing any discrepancies, the next step is to execute the migration process. 
Migrating data is a bulk-load operation that moves rows of data into SQL Server or SQL Azure in transactions. The number of rows to be loaded into SQL Server or SQL Azure in each transaction is configured in the project settings.

### Steps

To use SSMA for Access to migrate the data, perform the following steps.

1. Make sure you have **loaded the Access database objects** into SQL Server.

2. In Access Metadata Explorer, select the objects that contain the data that you want to migrate
    
    i. To migrate data for an entire database, select the check box next to the database name.
    ii. To migrate data from individual tables, expand the database, expand Tables, and then select the check box next to the table. To omit data from individual tables, clear the check box.
    
3. Right-click Databases and then select Migrate Data.

## Data sync and Cutover

With minimal-downtime migrations, the source you are migrating continues to change, drifting from the target in terms of data and schema, after the one-time migration occurs. During the **Data sync** phase, you need to ensure that all changes in the source are captured and applied to the target in near real time. After you verify that all changes in source have been applied to the target, you can cutover from the source to the target environment.

The Azure Database Migration Service does not yet support minimal-downtime migrations for this scenario, so the **Data sync** and **Cutover** phases are not currently applicable.
