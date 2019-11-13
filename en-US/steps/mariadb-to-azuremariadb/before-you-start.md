## Preparing for database migration

As you prepare for migrating your database to the cloud, verify that your source environment is supported and that you have addressed any prerequisites. This will help to ensure an efficient and successful migration.

### Overview

This scenario describes how to migrate a MariaDB instance to Azure Database for MariaDB.

There are two common ways to back up and restore databases to Azure Database for MariaDB. You can perform a dump and restore:

* From the command line, using mysqldump
* Using PHPMyAdmin.

### Common uses for dump and restore

You may use MySQL utilities such as mysqldump and mysqlpump to dump and load databases into an Azure Database for MariaDB server in several common scenarios.

* Use database dumps when you are migrating the entire database. This recommendation holds when moving a large amount of data, or when you want to minimize service interruption for live sites or applications.
* Make sure all tables in the database use the InnoDB storage engine when loading data into Azure Database for MariaDB. Azure Database for MariaDB supports only InnoDB Storage engine, and therefore does not support alternative storage engines. If your tables are configured with other storage engines, convert them into the InnoDB engine format before migration to Azure Database for MariaDB.

  For example, if you have a WordPress or WebApp using the MyISAM tables, first convert those tables by migrating into InnoDB format before restoring to Azure Database for MariaDB. Use the clause ENGINE=InnoDB to set the engine used when creating a new table, then transfer the data into the compatible table before the restore.

  ```
  INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
  ```

* To avoid any compatibility issues, use same version of MariaDB on the source and destination systems when dumping databases. For example, if your existing MariaDB server is version 10.2, then migrate to Azure Database for MariaDB configured to run version 10.2. The mysql_upgrade command does not function in an Azure Database for MariaDB server and is not supported. If you need to upgrade across MariaDB versions, first dump or export your lower version database into a higher version of MariaDB in your own environment. Then run mysql_upgrade before attempting migration to Azure Database for MariaDB.

### Use common tools

Use common utilities and tools such as MySQL Workbench, mysqldump, Toad, or Navicat to remotely connect and restore data into Azure Database for MariaDB. Use such tools on your client machine with an internet connection to connect to the Azure Database for MariaDB. Use an SSL encrypted connection for best security practices, see also [Configure SSL connectivity in Azure Database for MariaDB](https://docs.microsoft.com/azure/mariadb/concepts-ssl-connection-security). You do not need to move the dump files to any special cloud location when migrating to Azure Database for MariaDB.

### Performance considerations

To optimize performance when dumping large databases, consider the following:

* Use the exclude-triggers option in mysqldump when dumping databases. Exclude triggers from dump files to avoid the trigger commands firing during the data restore.
* Use the single-transaction option to set the transaction isolation mode to REPEATABLE READ and sends a START TRANSACTION SQL statement to the server before dumping data. Dumping many tables within a single transaction causes some extra storage to be consumed during restore. The single-transaction option and the lock-tables option are mutually exclusive because LOCK TABLES causes any pending transactions to be committed implicitly. To dump large tables, combine the single-transaction option with the quick option.
* Use the extended-insert multiple-row syntax that includes several VALUE lists. This results in a smaller dump file and speeds up inserts when the file is reloaded.
* Use the order-by-primary option in mysqldump when dumping databases, so that the data is scripted in primary key order.
* Use the disable-keys option in mysqldump when dumping data, to disable foreign key constraints before load. Disabling foreign key checks provides performance gains. Enable the constraints and verify the data after the load to ensure referential integrity.
* Use partitioned tables when appropriate.
* Load data in parallel. Avoid too much parallelism that would cause you to hit a resource limit, and monitor resources using the metrics available in the Azure portal.
* Use the defer-table-indexes option in mysqlpump when dumping databases, so that index creation happens after tables data is loaded.
* Copy the backup files to an Azure blob/store and perform the restore from there, which should be a lot faster than performing the restore across the Internet.

### Overview of prerequisites

Before beginning your migration project, it is important to address the associated prerequisites. When upgrading from MariaDB to Azure Database for MariaDB, you need to:

* [Create Azure Database for MariaDB server - Azure portal](https://docs.microsoft.com/azure/mariadb/quickstart-create-mariadb-server-database-using-azure-portal).
* Install the [mysqldump](https://mariadb.com/kb/en/library/documentation/clients-utilities/backup-restore-and-import-clients/mysqldump/) command-line utility on a computer.
* Have access to [MySQL Workbench](https://dev.mysql.com/downloads/workbench/), Toad, Navicat, or other third-party MySQL tool to do dump and restore commands.

### Additional resources

* For a current listing of supported versions, see the article [Supported MariaDB database versions](https://docs.microsoft.com/azure/mariadb/concepts-supported-versions).
* For detail on alternatives for migrating to Azure, see the white paper [Choosing your database migration path to Azure](https://aka.ms/dbmigratewp).
* Be sure to check out the [Azure Total Cost of Ownership (TCO) Calculator](https://aka.ms/azure-tco) to help estimate the cost savings you can realize by migrating your workloads to Azure.
* For a matrix of the Microsoft and third-party services and tools that are available to assist you with various database and data migration scenarios as well as specialty tasks, see the article [Service and tools for data migration](https://docs.microsoft.com/azure/dms/dms-tools-matrix).
* For an overview of the Azure Database Migration Guide and the information it contains, see the video [How to Use the Database Migration Guide](https://azure.microsoft.com/resources/videos/how-to-use-the-azure-database-migration-guide/).
