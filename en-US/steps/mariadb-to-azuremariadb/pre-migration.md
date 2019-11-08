## Pre-migration overview

After verifying that your source environment is supported and ensuring that you have addressed any prerequisites, you are ready to start the Pre-migration stage. This part of the process involves conducting an inventory of the databases that you need to migrate, assessing those databases for potential migration issues or blockers, and then resolving any items you might have uncovered.

## Discover

The goal of the Discover phase is to identify existing data sources and details about the features that are being used to get a better understanding of and plan for the migration. This process involves identifying all your organization’s MariaDB instances along with the version and features in use.

## Assess

When the data sources have been identified, the next step is generally to assess the source MariaDB instance(s) migrating to Azure Database for MariaDB to understand the gaps between the source and target instances.

## Convert

For heterogenous migrations (such as Oracle to Azure Database for PostgreSQL), the Pre-migration stage also involves converting the schema(s) in the source database(s) to be compatible with the target environment. For homogenous migrations, such as MariaDB to Azure Database for MariaDB, conversion of the source schema to work in the target environment is not required.
