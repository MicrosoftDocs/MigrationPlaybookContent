## Migration overview

After you have the necessary prerequisites in place and have completed any tasks associated with the Pre-migration stage, you are ready to perform the schema and data migration, or in this case, to create a backup of your source MariaDB database and restore it to a database in Azure Database for MariaDB.

## Backup and restore using mysqldump

You can use mysqldump to back up and restore a MariaDB database.

### Create a backup file

To back up an existing MariaDB database on the local on-premises server or in a virtual machine, run the following command using mysqldump:

  ```
  $ mysqldump --opt -u [uname] -p[pass] [dbname] > [backupfile.sql]
  ```

The parameters to provide are:
* [uname] Your database username
* [pass] The password for your database (note there is no space between -p and the password)
* [dbname] The name of your database
* [backupfile.sql] The filename for your database backup
* [--opt] The mysqldump option

For example, to back up a database named 'testdb' on your MariaDB server with the username 'testuser' and with no password to a file testdb_backup.sql, use the following command. The command backs up the testdb database into a file called testdb_backup.sql, which contains all the SQL statements needed to re-create the database.

```
$ mysqldump -u root -p testdb > testdb_backup.sql
```

To select specific tables in your database to back up, list the table names separated by spaces. For example, to back up only table1 and table2 tables from the 'testdb', follow this example:

```
$ mysqldump -u root -p testdb table1 table2 > testdb_tables_backup.sql
```

To back up more than one database at once, use the --database switch and list the database names separated by spaces.

```
$ mysqldump -u root -p --databases testdb1 testdb3 testdb5 > testdb135_backup.sql 
```

### Create a database on the target server

Create an empty database on the target Azure Database for MariaDB server where you want to migrate the data. Use a tool such as MySQL Workbench, Toad, or Navicat to create the database. The database can have the same name as the database contained the dumped data or you can create a database with a different name.

To get connected, in the Azure portal, locate the connection information in the **Overview** blade of your Azure Database for MariaDB instance.

![Overview blade - Azure Database for MariaDB](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mariadb-to-azuremariadb/mariadboverviewblade.png)  

Add the connection information into your MySQL Workbench.

![MySQL Workbench screen](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mariadb-to-azuremariadb/mysqlworkbench.png)  
 
### Restore your MariaDB database

After you have created the target database, you can use the mysql command or MySQL Workbench to restore the data into the specific newly created database from the dump file.

```
mysql -h [hostname] -u [uname] -p[pass] [db_to_restore] < [backupfile.sql]
```

In this example, restore the data into the newly created database on the target Azure Database for MariaDB server.

```
$ mysql -h mydemoserver.mariadb.database.azure.com -u myadmin@mydemoserver -p testdb < testdb_backup.sql
```

## Backup and restore using phpMyAdmin

You can use phpMyAdmin to back up and restore a MariaDB database.

### Export using phpMyAdmin

To export, you can use the common tool phpMyAdmin, which you may already have installed locally in your environment. To export your MariaDB database using phpMyAdmin:
1. In phpMyAdmin, in the list on the left, select the database name.
2. Select **Export**.
   A new page appears to view the dump of database.

3. In the **Export** area, select **Select All** to choose the tables in your database.
4. In the **SQL options** area, select the appropriate options.
5. Select **Save as file** and the corresponding compression option, and then select **Go**.

  A dialog box should appear prompting you to save the file locally.

### Import using phpMyAdmin

Importing your database is similar to exporting. To import your MariaDB data using phpMyAdmin:

1. In phpMyAdmin, on the **phpMyAdmin setup** page, select **Add**, and then provide the connection details and login information for your Azure Database for MariaDB server.
2. Create an appropriately named database and select it on the left of the screen.
  To rewrite the existing database, select the database name, select all the check boxes beside the table names, and then select **Drop** to delete the existing tables.

3. Select **SQL** to display a page on which you can type in SQL commands, or upload your SQL file.
4. Select **browse** to find the database file.
5. Select **Go** to export the backup, execute the SQL commands, and then re-create your database.
