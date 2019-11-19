## Pre-migration overview

As you prepare for migrating to the cloud, verify that your source environment is supported and that you have addressed any prerequisites. This will help to ensure an efficient and successful migration.

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
<p><a href="https://aka.ms/dmj-wp-mainframe-optimize">Optimization Guide for Mainframe App/Data recompiled to .NET &amp; SQL Server</a></p>
</td>
<td width="59%">
<p>This guide offers optimization advice for executing point-lookups against SQL Server from .NET as efficiently as possible. Customers wishing to migrate from mainframe databases to SQL Server may desire to migrate existing mainframe-optimized design patterns, especially when using 3rd party tools (such as Raincode Compiler) to automatically migrate mainframe code (COBOL/JCL etc) to T-SQL and C# .NET.</p>
</td>
</tr>
</tbody>
</table>

**Note**: These resources were developed as part of the Data Migration Jumpstart Program (DM Jumpstart), which is sponsored by the Azure Data Group engineering team. The core charter DM Jumpstart is to unblock and accelerate complex modernization and compete data platform migration opportunities to Microsoft’s Azure Data platform. If you think your organization would be interested in participating in the DM Jumpstart program, please contact your account team and ask that they submit a nomination.

### Additional resources

* For an overview of the Azure Database Migration Guide and the information it contains, see the video [How to Use the Database Migration Guide](https://azure.microsoft.com/resources/videos/how-to-use-the-azure-database-migration-guide/).
* For a walk through of the phases of the migration process and detail about the specific tools and services recommended to perform assessment and migration, see the video [Overview of the migration journey and the tools/services recommended for performing assessment and migration](https://azure.microsoft.com/resources/videos/overview-of-migration-and-recommended-tools-services/).

## Assess and Convert

### Overview

By using SQL Server Migration Assistant (SSMA) for SAP Adaptive Server Enterprise (formally SAP Sybase ASE) you can review database objects and data, assess databases for migration, migrate Sybase database objects to SQL Server, and then migrate data to SQL Server.

**Note**: For more information about SSMA, see the article [SQL Server Migration Assistant for Sybase (SybaseToSQL)](https://docs.microsoft.com/en-us/sql/ssma/sybase/sql-server-migration-assistant-for-sybase-sybasetosql).

### Steps

To use SSMA for SAP ASE to create an assessment, perform the following steps.

1.Download **[SSMA for Sybase](https://www.microsoft.com/en-us/download/details.aspx?id=54256)**, and then install it.

_SSMA is now ready for use._

2.Assess the source database and discover conversion rate and effort to resolve issues. For more information about SSMA for Sybase Assessments, see the article [Assessing Sybase ASE Database Objects for Conversion (SybaseToSQL)](https://docs.microsoft.com/en-us/sql/ssma/sybase/assessing-sybase-ase-database-objects-for-conversion-sybasetosql).

_This will generate an Assessment Report which shows the results of the conversion of database objects to Transact-SQL syntax, and can also help you estimate the complexity and cost of your migration projects._

3.Converting Sybase Schemas. For more information about SSMA for Sybase Conversion, see the article [Converting Sybase ASE Database Objects (SybaseToSQL)](https://docs.microsoft.com/en-us/sql/ssma/sybase/converting-sybase-ase-database-objects-sybasetosql).

_When the schema conversion is complete, you are ready to move on to the Migration phase._

**Note**: For complete step-by-step guidance on installing and using SSMA for Sybase, see the following resources:

* The article [Installing SSMA for Sybase Client (SybaseToSQL)](https://docs.microsoft.com/en-us/sql/ssma/sybase/installing-ssma-for-sybase-client-sybasetosql).
* The article [Installing SSMA Components on SQL Server (SybaseToSQL)](https://docs.microsoft.com/en-us/sql/ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql).
* The blog posting [SQL Server Migration Assistant: How to assess and migrate data from non-Microsoft data platforms to SQL Server](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/).
