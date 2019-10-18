## Preparing for database migration

As you prepare for migrating your database to the cloud, verify that your source environment is supported and that you have addressed any prerequisites. This will help to ensure an efficient and successful migration.

### Overview
PostgreSQL is one of world’s most advanced open source databases. This article describes how to use the free ora2pg utility to migrate an Oracle database to PostgreSQL.
You can use ora2pg, a free tool, to migrate an Oracle or MySQL database to a PostgreSQL compatible schema. The utility connects your Oracle database, scans it automatically, and extracts its structure or data. Afterwards ora2pg generates SQL scripts that you can load into your PostgreSQL database.
ora2pg can be used for tasks from reverse engineering an Oracle database, performing a huge enterprise database migration, or simply replicating some Oracle data into a PostgreSQL database. It’s easy to use and doesn't require any Oracle database knowledge other than the ability to provide the parameters needed to connect to the Oracle database.

**Note**: For more information about using the latest version of ora2pg, see the [ora2pg documentation](https://ora2pg.darold.net/documentation.html).

### Typical ora2pg migration architecture

![ora2pg migration architecture](https://mpbdevcontent.azureedge.net/Images/scenario-assets/OracleToAzurePG/ora2pg_architecture.png)

After provisioning the VM and Azure Database for PostgreSQL, two configurations are needed for enabling connectivity between them: “Allow Azure Services” and “Enforce SSL Connection”, depicted as follows:
- “Connection Security” blade -> Allow access to Azure Services -> ON 
- “Connection Security” blade -> SSL Settings -> Enforce SSL Connection -> DISABLED 

### Prerequisites

1. Before installing ora2pg, be sure to install the corresponding Oracle and PostgreSQL drivers.
2. Download the latest version of the ora2pg tool, and then install it.

### Migration recommendations

- To improve the performance of the assessment or export operations in the Oracle server, collect statistics as following:

    ```
    BEGIN 
            DBMS_STATS.GATHER_SCHEMA_STATS 
            DBMS_STATS.GATHER_DATABASE_STATS  
            DBMS_STATS.GATHER_DICTIONARY_STATS 
            END; 
    ```

- Export data using the COPY command instead of INSERT.
- Avoid exporting tables with their FKs, constraints, and indexes – doing so will make it slower to import the data into PostgreSQL.
- Create materialized views using the “no data clause” and refresh it later.
- If possible, implement unique indexes in materialized views, this will make the refresh faster with the syntax “REFRESH MATERIALIZED VIEW CONCURRENTLY”.

### Migration assets from real-world engagements

For additional assistance with completing this migration scenario, please see the following resources, which were developed in support of a real-world migration project engagement.

<br>
<table width="100%">
<thead>
<tr>
<th width="18%">
<p><strong>Title/link</strong></p>
</th>
<th width="59%">
<p><strong>Description</strong></p>
</th>
</tr>
</thead>
<tbody>
<tr>
<td width="18%">
<p><a href="https://github.com/Microsoft/DataMigrationTeam/blob/master/Whitepapers/Oracle%20to%20Azure%20PostgreSQL%20Migration%20Cookbook.pdf">Oracle to Azure PostgreSQL Migration Cookbook</a></p>
</td>
<td width="59%">
<p>This document purpose is to provide Architects, Consultants, DBAs and related roles with a guide for quickly migrating workloads from Oracle to Azure Database for PostgreSQL using ora2pg tool.</p>
</td>
</tr>
<tr>
<td width="18%">
<p><a href="https://github.com/Microsoft/DataMigrationTeam/blob/master/Whitepapers/Oracle%20to%20Azure%20Database%20for%20PostgreSQL%20Migration%20Workarounds.pdf">Oracle to Azure PostgreSQL Migration Workarounds</a></p>
</td>
<td width="59%">
<p>This document purpose is to provide Architects, Consultants, DBAs and related roles with a guide for quick fixing / working around issues while migrating workloads from Oracle to Azure Database for PostgreSQL.</p>
</td>
</tr>
<tr>
<td width="18%">
<p><a href="https://github.com/Microsoft/DataMigrationTeam/blob/master/Whitepapers/Steps%20to%20Install%20ora2pg%20on%20Windows.pdf">Steps to Install ora2pg on Windows</a></p>
</td>
<td width="59%">
<p>This document is meant to be used as a Quick Installation Guide for enabling migration of schema & data from Oracle to Azure Database for PostgreSQL using ora2pg tool on Windows. Complete details on the tool can be found at http://ora2pg.darold.net/documentation.html. </p>
</td>
</tr>
<tr>
<td width="18%">
<p><a href="https://github.com/Microsoft/DataMigrationTeam/blob/master/Whitepapers/Steps%20to%20Install%20ora2pg%20on%20Linux.pdf">Steps to Install ora2pg on Linux</a></p>
</td>
<td width="59%">
<p>This document is meant to be used as a Quick Installation Guide for enabling migration of schema & data from Oracle to Azure Database for PostgreSQL using ora2pg tool on Linux. Complete details on the tool can be found at http://ora2pg.darold.net/documentation.html. </p>
</td>
</tr>
</tbody>
</table>

**Note**: These resources were developed as part of the Data Migration Jumpstart Program (DM Jumpstart), which is sponsored by the Azure Data Group engineering team. The core charter DM Jumpstart is to unblock and accelerate complex modernization and compete data platform migration opportunities to Microsoft’s Azure Data platform. If you think your organization would be interested in participating in the DM Jumpstart program, please contact your account team and ask that they submit a nomination.

### Additional resources

- [Azure Database for PostgreSQL documentation](https://docs.microsoft.com/azure/postgresql/).
- [ora2pg documentation](https://ora2pg.darold.net/documentation.html).
- [PostgreSQL website](https://www.postgresql.org/).
- [Autonomous transaction support in PostgreSQL](http://blog.dalibo.com/2016/08/19/Autonoumous_transactions_support_in_PostgreSQL.html) blog post.
- For a matrix of the Microsoft and third-party services/tools available to assist you with various database and data migration scenarios (and specialty tasks), see the article [Service and tools for data migration](https://docs.microsoft.com/azure/dms/dms-tools-matrix).

**Videos**

- For an overview of the Azure Database Migration Guide and the information it contains, see the video [How to Use the Database Migration Guide](https://azure.microsoft.com/resources/videos/how-to-use-the-azure-database-migration-guide/).
- For a walk through of the phases of the migration process and detail about the specific tools and services recommended to perform assessment and migration, see the video [Overview of the migration journey and the tools/services recommended for performing assessment and migration](https://azure.microsoft.com/resources/videos/overview-of-migration-and-recommended-tools-services/).

### Contact support

If you need assistance with your migrations beyond the ora2pg tooling, contact the [@Ask Azure DB for PostgreSQL](mailto:AskAzureDBforPostgreSQL@service.microsoft.com) alias for information about other migration options.
