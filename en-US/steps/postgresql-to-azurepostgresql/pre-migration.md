## Pre-migration overview

As you prepare for migrating to the cloud, verify that your source environment is supported and that you have addressed any prerequisites. This will help to ensure an efficient and successful migration.

### Additional resources

- For a matrix of the Microsoft and third-party services and tools that are available to assist you with various database and data migration scenarios as well as specialty tasks, see the article [Service and tools for data migration](https://docs.microsoft.com/azure/dms/dms-tools-matrix).
- For an overview of the Azure Database Migration Guide and the information it contains, see the video [How to Use the Database Migration Guide](https://azure.microsoft.com/resources/videos/how-to-use-the-azure-database-migration-guide/).
- For a walk through of the phases of the migration process and detail about the specific tools and services recommended to perform assessment and migration, see the video [Overview of the migration journey and the tools/services recommended for performing assessment and migration](https://azure.microsoft.com/resources/videos/overview-of-migration-and-recommended-tools-services/).
- For a demo of how to migrate a PostgreSQL database running in an on-premises virtual machine to Azure Database for PostgreSQL with minimum downtime using the Azure CLI, see the video [How to migrate PostgreSQL to Azure Database for PostgreSQL with minimum downtime using DMS and the Azure CLI](https://azure.microsoft.com/resources/videos/how-to-migrate-postgresql-to-azure-postgresql-online-dms-and-cli/).
- For a walk through of the detailed workflow and a demo that shows how to migrate your application using minimal downtime to Azure Database for PostgreSQL, see the video [Migrate your PostgreSQL applications to Azure with minimal downtime using the Azure Database Migration Service](https://azure.microsoft.com/resources/videos/postg-migrate-vid/).

## Evaluation

Migrating an on-premises PostgreSQL instance, a PostgreSQL instance hosted in a virtual machine, or an RDS PostgreSQL instance to Azure Database for PostgreSQL is considered a homogeneous migration. Microsoft aims to support the currently released major version (n) and the two prior major versions (-2), or n-2. Azure Database for PostgreSQL supports versions 9.5.7 and 9.6.2, and if your on-premises PostgreSQL instance is running one of these versions, the database will be fully compatible, and the migration will be relatively straightforward.

If you use extensions in PostgreSQL, please see the article [PostgreSQL extensions in Azure Database for PostgreSQL](https://docs.microsoft.com/en-us/azure/postgresql/concepts-extensions).
