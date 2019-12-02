## Preparing for database migration

As you prepare for migrating your database to the cloud, verify that your source environment is supported and that you have addressed any prerequisites. This will help to ensure an efficient and successful migration.

## Overview

This scenario describes how to migrate a MySQL instance to Azure Database for MySQL.

## Offline versus online migrations

For selected migration scenarios, Azure Database Migration Service supports both offline and online migrations. With an offline migration, application downtime begins when the migration starts. For an online migration, downtime is limited to the time required to cut over to the new environment when the migration completes.

**Important**: With MySQL to Azure Database for MySQL migrations, Azure Database Migration Service supports online migrations only.

## Supported versions

This section describes all supported scenarios and options for an upgrade from on-premises MySQL versions to Azure Database for MySQL. This information is current as of December 2019.

Details for migrations to Azure Database for MySQL from the following MySQL sources are included:

* MySQL 5.6
* MySQL 5.7

You can migrate MySQL running on-premises or on AWS RDS.

## Overview of prerequisites

Before beginning your migration project, it is important to address the associated prerequisites for leveraging Azure Database Migration Service (DMS) for migrations. When upgrading from MySQL to Azure Database for MySQL, there are prerequisites associated with:

* Creating and instance of Azure Database for MySQL (detail [here](https://docs.microsoft.com/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal)).
* Creating an instance of Azure Database Migration Service (detail [here](https://docs.microsoft.com/azure/dms/pre-reqs)).
* Using Azure Database Migration Service to perform online migrations from:
  * MySQL (detail [here](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online#prerequisites)).
  * RDS MySQL (detail [here](https://docs.microsoft.com/azure/dms/tutorial-rds-mysql-server-azure-db-for-mysql-online)).

## Additional resources

* For a matrix of the Microsoft and third-party services and tools that are available to assist you with various database and data migration scenarios as well as specialty tasks, see the article [Service and tools for data migration](https://docs.microsoft.com/azure/dms/dms-tools-matrix).
* For an overview of the Azure Database Migration Guide and the information it contains, see the video [How to Use the Database Migration Guide](https://azure.microsoft.com/resources/videos/how-to-use-the-azure-database-migration-guide/).
* For a walk through of the phases of the migration process and detail about the specific tools and services recommended to perform assessment and migration, see the video [Overview of the migration journey and the tools/services recommended for performing assessment and migration](https://azure.microsoft.com/resources/videos/overview-of-migration-and-recommended-tools-services/).
