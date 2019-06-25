## Pre-migration overview

As you prepare for migrating to the cloud, verify that your source environment is supported and that you have address any prerequisites to help ensure a successful migration.

### Additional resources

- For a matrix of the Microsoft and third-party services and tools that are available to assist you with various database and data migration scenarios as well as specialty tasks, see the article [Service and tools for data migration](https://docs.microsoft.com/azure/dms/dms-tools-matrix).
- For an overview of the Azure Database Migration Guide and the information it contains, see the video [How to Use the Database Migration Guide](https://azure.microsoft.com/resources/videos/how-to-use-the-azure-database-migration-guide/).
- For a walk through of the phases of the migration process and detail about the specific tools and services recommended to perform assessment and migration, see the video [Overview of the migration journey and the tools/services recommended for performing assessment and migration](https://azure.microsoft.com/resources/videos/overview-of-migration-and-recommended-tools-services/).

## Evaluation

Migrating from an on-premises instance of MySQL, a MySQL instance hosted in a virtual machine, or an RDS MySQL instance to Azure Database for MySQL is considered a homogeneous migration. Azure Database for MySQL automatically manages patching for minor version updates. Azure Database for MySQL supports versions 5.6.3.5 and 5.7.1.8 using the InnoDB engine, so if you are running a supported version in on-premises MySQL, the database will be fully compatible, and the migration will be relatively straightforward.

If you have MyISAM tables, convert them to InnoDB before you migrate them to Azure Database for MySQL. For more information, see the MySQL article [Converting Tables from MyISAM to InnoDB](https://dev.mysql.com/doc/refman/5.6/en/converting-tables-to-innodb.html).