## Pre-migration overview

After verifying that your source environment is supported and ensuring that you have addressed any prerequisites, you are ready to start the Pre-migration stage. This part of the process involves conducting an inventory of the databases that you need to migrate, assessing those databases for potential migration issues or blockers, and then resolving any items you might have uncovered. For heterogenous migrations (such as Oracle to Azure Database for PostgreSQL), this stage also involves converting the schema(s) in the source database(s) to be compatible with the target environment. For homogenous migrations, such as SQL Server to Azure SQL Database, conversion of the source schema to work in the target environment is not required.

## Discover

The goal of the Discover phase is to identify existing data sources and details about the features that are being used to get a better understanding of and plan for the migration. This process involves scanning the network to identify all your organization’s SQL Server instances together with the version and features in use.

You can use the [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-overview) service to assesses on-premises workloads for migration to Azure. The service assesses the migration suitability of on-premises computers, performs performance-based sizing, and provides cost estimations for running on-premises computers in Azure. If you're contemplating lift-and-shift migrations, or are in the early assessment stages of migration, this service is for you.

You can also use the [Microsoft Assessment and Planning Toolkit](https://www.microsoft.com/en-us/download/details.aspx?id=7826) (the "MAP Toolkit") to assess your current IT infrastructure for a variety of technology migration projects. This Solution Accelerator provides a powerful inventory, assessment, and reporting tool to simplify the migration planning process.

For more information about the tools available for use during the Discover phase, see the article [Services and tools available for data migration scenarios](https://docs.microsoft.com/azure/dms/dms-tools-matrix).

## Assess

When the data sources have been identified, the next step is to assess on-premises SQL Server instance(s) migrating to Azure SQL database(s) to understand the gaps between the source and target instances. Use the Data Migration Assistant (DMA) to assess your source database before migrating to Azure SQL Database.

### Overview of assessment steps

An overview of the steps associated with using DMA to create an assessment follows.

1. Open the Data Migration Assistant (DMA), and then begin creating a new assessment project.

2. Specify a project name, select **SQL Server** as the source server type, and then select **Azure SQL Database** as the target server type.

3. Select the type(s) of assessment reports (database compatibility and feature parity) that you want to generate.
    - The SQL Server feature parity category provides a comprehensive set of recommendations, alternative approaches available in Azure, and mitigating steps to help you plan the effort into your migration projects.
    - The Compatibility issues category identifies partially supported or unsupported features that reflect compatibility issues that might block migrating on-premises SQL Server database(s) to an Azure SQL Database managed instance. Recommendations are also provided to help you address those issues.

4. Specify the source connection details for your SQL Server, connect to the source database, and then start the assessment.

5. When the process is complete, review the assessment reports for migration blocking issues and feature parity issues by selecting the specific options.

6. Determine the database compatibility level that you want to minimize your efforts after migrating to Azure SQL Database.

7. Identify the best Azure SQL Database managed instance SKU for your on-premises workload.

For additional detail on this process, see the article [Perform a SQL Server migration assessment with Data Migration Assistant](https://docs.microsoft.com/en-us/sql/dma/dma-assesssqlonprem?view=sql-server-2017).

## Convert

After assessing the source database instance(s) you are migrating, for heterogenous migrations, you need to convert the schema to work in the target environment. Since migrating from SQL Server to Azure SQL Database is a homogeneous migration, the Convert phase is unnecessary.
