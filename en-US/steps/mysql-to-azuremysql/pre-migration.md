## Pre-migration overview

After verifying that your source environment is supported and ensuring that you have addressed any prerequisites, you are ready to start the **Pre-migration** stage. This part of the process involves conducting an inventory of the databases that you need to migrate, assessing those databases for potential migration issues or blockers, and then resolving any items you might have uncovered. For heterogenous migrations (such as Oracle to Azure Database for PostgreSQL), this stage also involves converting the schema(s) in the source database(s) to be compatible with the target environment. For homogenous migrations, such as MySQL to Azure Database for MySQL, conversion of the source schema to work in the target environment is not required.

## Evaluation

Migrating from an on-premises instance of MySQL, a MySQL instance hosted in a virtual machine, or an RDS MySQL instance to Azure Database for MySQL is considered a homogeneous migration. Azure Database for MySQL automatically manages patching for minor version updates. Azure Database for MySQL supports a variety of MySQL versions using the InnoDB engine. If you are running a supported version of on-premises MySQL, the database will be fully compatible and the migration will be relatively straightforward.

For a current listing of supported versions, see the article [Supported MySQL database versions](https://docs.microsoft.com/azure/mysql/concepts-supported-versions).

If you have MyISAM tables, convert them to InnoDB before you migrate them to Azure Database for MySQL. For more information, see the MySQL article [Converting Tables from MyISAM to InnoDB](https://dev.mysql.com/doc/refman/5.6/en/converting-tables-to-innodb.html).
