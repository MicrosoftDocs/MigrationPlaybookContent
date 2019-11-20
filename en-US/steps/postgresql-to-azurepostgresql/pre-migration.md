## Pre-migration overview

After verifying that your source environment is supported and ensuring that you have addressed any prerequisites, you are ready to start the **Pre-migration** stage. This part of the process involves conducting an inventory of the databases that you need to migrate, assessing those databases for potential migration issues or blockers, and then resolving any items you might have uncovered. For heterogenous migrations (such as Oracle to Azure Database for PostgreSQL), this stage also involves converting the schema(s) in the source database(s) to be compatible with the target environment. For homogenous migrations, such as PostgreSQL to Azure Database for PostgreSQL, conversion of the source schema to work in the target environment is not required.

## Evaluation

Migrating an on-premises PostgreSQL instance, a PostgreSQL instance hosted in a virtual machine, or an RDS PostgreSQL instance to Azure Database for PostgreSQL is considered a homogeneous migration. Microsoft aims to support the currently released major version (n) and the two prior major versions (-2), or n-2. Azure Database for PostgreSQL supports a variety of versions of PostgreSQL. If your on-premises PostgreSQL instance is running a supported version, the database will be fully compatible and the migration will be relatively straightforward.

For a current listing of supported versions, see the article [Supported PostgreSQL database versions](https://docs.microsoft.com/azure/postgresql/concepts-supported-versions).

If you use extensions in PostgreSQL, please see the article [PostgreSQL extensions in Azure Database for PostgreSQL](https://docs.microsoft.com/en-us/azure/postgresql/concepts-extensions).
