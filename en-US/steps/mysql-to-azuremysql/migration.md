## Migration overview

After you have the necessary prerequisites in place and have completed the tasks associated with the **Pre-migration** stage, you are ready to perform the schema and data migration.

## Migrate schema and data

The first step in migrating from an on-premises instance of MySQL or a MySQL instance hosted in a virtual machine is to migrate the **schema** to Azure Database for MySQL. After the schema(s) is deployed, the next step is to migrate the data.

There are two ways to migrate the schema and data from a MySQL database to Azure Database for MySQL.

- **For relatively large databases that can’t afford downtime during migration**, see the detailed, step-by-step instructions in the article [Migrate MySQL to Azure Database for MySQL online using DMS](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online).

- **For relatively small (<150GB for example) databases that allow for downtime during migration**, you can use MySQL Workbench to migrate the scheman, and then use dump and restore via MySQL Workbench and the mysqldump utility to migrate the data.

**Steps**

For MySQL migrations that do not require minimal downtime, the easiest way to migrate the schema is to use MySQL Workbench configured to migrate only the schema by performing the following steps:

1.	Download [MySQL Workbench](https://www.mysql.com/products/workbench/), and then install it.

2.	Start MySQL Workbench, and then enter the source MySQL instance and the target Azure Database for MySQL environment.
 
 ![Image Alt Text MySQL RDBMS Sources](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mysql-to-azuremysql/1-mysql_RDBMS_Sources.png)

 ![Image Alt Text MySQL RDBMS Targets](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mysql-to-azuremysql/2-mysql_RDBMS_Targets.png)
 
3.	Select the database schema(s) that you want to migrate:

 ![Image Alt Text MySQL Select Schema](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mysql-to-azuremysql/3_mysql_select_schema.png)
 
4.	Select all the tables, views, and routines that are appropriate for migration, and then select **Next**.

 ![Image Alt Text MySQL Select Objects](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mysql-to-azuremysql/4-mysql_select_objects.png)

5.	Evaluate the schema script and manually edit it, if necessary, and then select **Next** to execute the schema creation script.

    **Note**: Be sure to remove any CREATE DEFINER commands manually or by using the --skip-definer command when performing a mysqldump. DEFINER requires super privileges to create and is restricted in Azure Database for MySQL.

 ![Image Alt Text MySQL Run Schema Creation](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mysql-to-azuremysql/5-mysql_run_schema_creation.png)

6.	Evaluate the result of schema deployment in the next screen, and then close the migration wizard in MySQL Workbench.

After the schema is migrated, to migrate the data, refer to the article [Dump and restore](https://docs.microsoft.com/azure/mysql/concepts-migrate-dump-restore) in the Azure Database for MySQL documentation.

## Data sync and Cutover

With minimal-downtime migrations, the source you are migrating continues to change, drifting from the target in terms of data and schema, after the one-time migration occurs. During the **Data sync** phase, you need to ensure that all changes in the source are captured and applied to the target in near real time. After you verify that all changes in source have been applied to the target, you can cutover from the source to the target environment.

For details on Data Sync and Cutover for this scenario, see the instructions in the [Perform migration cutover](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online#perform-migration-cutover) section of the article Migrate MySQL to Azure Database for MySQL online using DMS.
