## Pre-migration overview

As you prepare for migrating to the cloud, verify that your source environment is supported and that you have address any prerequisites to help ensure a successful migration.

### Migration learnings and best practices from real-world engagements

For additional assistance with completing this migration scenario, please see the following resources, which were developed in support of a real-world migration project engagement.

<br>
<table width="100%">
<thead>
<tr>
<td width="18%">
<p><strong>Title/link</strong></p>
</td>
<td width="59%">
<p><strong>Description</strong></p>
</td>
</tr>
</thead>
<tbody>
<tr>
<td width="18%">
<p><a href="https://github.com/Microsoft/DataMigrationTeam/tree/master/Data%20Workload%20Assessment%20Model%20and%20Tool">Data Workload Assessment Model and Tool</a></p>
</td>
<td width="59%">
<p>This tool provides suggested &ldquo;best fit&rdquo; target platforms, cloud readiness, and application/database remediation level for a given workload. It offers simple, one-click calculation and report generation that greatly helps to accelerate large estate assessments by providing and automated and uniform target platform decision process.</p>
</td>
</tr>
<tr>
<td width="18%">
<p><a href="https://github.com/Microsoft/DataMigrationTeam/tree/master/DB2%20zOS%20Data%20Assets%20Discovery%20and%20Assessment%20Package">DB2 zOS Data Assets Discovery and Assessment Package</a></p>
</td>
<td width="59%">
<p>After running the SQL script on a database, you can export the results to a file on the file system. Several file formats are supported, including *.csv, so that you can capture the results in external tools such as spreadsheets. This method can be useful if you want to more easily share results information with team who do not have the workbench installed.</p>
</td>
</tr>
<tr>
<td width="18%">
<p><a href="https://github.com/Microsoft/DataMigrationTeam/tree/master/IBM%20DB2%20LUW%20Inventory%20Scripts%20and%20Artifacts">IBM DB2 LUW Inventory Scripts and Artifacts</a></p>
</td>
<td width="59%">
<p>This asset includes a SQL query that hits IBM DB2 LUW version 11.1 system tables and provides a count of objects by schema and object type, a rough estimate of &lsquo;Raw Data&rsquo; in each schema, and the sizing of tables in each schema, with results stored in a CSV format.</p>
</td>
</tr>
<tr>
<td width="18%">
<p><a href="https://aka.ms/dmj-wp-db2-purescale">DB2 LUW Pure Scale on Azure - Setup Guide</a></p>
</td>
<td width="59%">
<p>This guide serves as a starting point for a DB2 implementation plan. While business requirements will differ, the same basic pattern applies. This architectural pattern may also be used for OLAP applications on Azure.</p>
</td>
</tr>
</tbody>
</table>

**Note**: These resources were developed as part of the Data Migration Jumpstart Program (DM Jumpstart), which is sponsored by the Azure Data Group engineering team. The core charter DM Jumpstart is to unblock and accelerate complex modernization and compete data platform migration opportunities to Microsoft’s Azure Data platform. If you think your organization would be interested in participating in the DM Jumpstart program, please contact your account team and ask that they submit a nomination.

### Additional resources

- Be sure to check out the [Azure Total Cost of Ownership (TCO) Calculator](https://aka.ms/azure-tco) to help estimate the cost savings you can realize by migrating your workloads to Azure.
- For a matrix of the Microsoft and third-party services and tools that are available to assist you with various database and data migration scenarios as well as specialty tasks, see the article [Service and tools for data migration](https://docs.microsoft.com/azure/dms/dms-tools-matrix).

**Videos**

- For an overview of the Azure Database Migration Guide and the information it contains, see the video [How to Use the Database Migration Guide](https://azure.microsoft.com/resources/videos/how-to-use-the-azure-database-migration-guide/).
- For a walk through of the phases of the migration process and detail about the specific tools and services recommended to perform assessment and migration, see the video [Overview of the migration journey and the tools/services recommended for performing assessment and migration](https://azure.microsoft.com/resources/videos/overview-of-migration-and-recommended-tools-services/).

## Discover

The goal of the Discover phase is to identify existing data sources and details about the features that are being used to get a better understanding of and plan for the migration. This process involves scanning your network to identify all your organization’s DB2 instances together with the version and features in use.

## Assess and Convert

To use SSMA for DB2 to create an assessment, perform the following steps.

### Steps

1. **Download [SSMA for DB2]( https://www.microsoft.com/en-us/download/details.aspx?id=54254)**, and then install it.

2. **Assess the source database** and discover conversion rate and effort to resolve issues.

   a.	Click on the "File" menu and choose "New Project". Provide the project name, a location to save your project and the migration target.

   b.   Select SQL Server from the “Migrate To” options
    
   c. Click "OK".

   ![New Project](https://mpbdevcontent.azureedge.net/Images/scenario-assets/ssmadb2newproject.png)

   d. Connect to the DB2 server by providing the connection details in the "Connect to DB2" dialog.
   
   ![Connect to DB2](https://mpbdevcontent.azureedge.net/Images/scenario-assets/ssmadb2connect.png)
   
   e.	Create the conversion report by selecting the DB2 schema in the "DB2 Metadata Explorer" by choosing "Create Report" from the right-click menu options or the menu bar on the top.
   
   ![Create Report](https://mpbdevcontent.azureedge.net/Images/scenario-assets/createreport.png)
   
   f.	This will generate an HTML report with conversion statistics and error/ warnings, if any. Analyze this report to understand conversion issues and its cause.
   
   ![Assessment Report](https://mpbdevcontent.azureedge.net/Images/scenario-assets/assessmentreport.png)
   
   g.	This report can also be accessed from the SSMA projects folder as selected in the first screen. From the example above locate the report.xml file 
   from: 
   
   *drive:*\Users\<username>\Documents\SSMAProjects\MyDB2Migration\report\report_2016_11_12T02_47_55\
   
   and open it in Excel to get an inventory of DB2 objects and the effort required to perform schema conversions.
   
3. **Perform schema conversion**.

   a. Before you perform schema conversion validate the default datatype mappings or change them based on requirements. You could do so either by navigating to the "Tools" menu and choosing "Project Settings" or you can change type mapping for each table by selecting the table in the "DB2 Metadata Explorer".
   
   ![Type Mappings](https://mpbdevcontent.azureedge.net/Images/scenario-assets/typemappings.png)
   
   b.	Dynamic or ad hoc queries can be added to the "Statements" node by selecting that node and choosing "Add Statement" from the right-click menu options.
   
   c.	For converting and moving the schema to SQL Server Database, connect to the SQL instance by providing the connection details in the "Connect to SQL Server" dialog. You can choose to connect to an existing database or provide a new name, in which case a database will be created on the target server.
   
   ![Connect to SQL](https://mpbdevcontent.azureedge.net/Images/scenario-assets/connecttosql.png)
   
   d.	Convert the schema by choosing "Convert Schema" from the right-click menu options or the menu bar on the top.
   
   ![Convert Schema](https://mpbdevcontent.azureedge.net/Images/scenario-assets/convertschema.png)
   
   e.	After the schema has converted compare and review the structure of the schema to identify potential problems.
   
   ![Convert Schema](https://mpbdevcontent.azureedge.net/Images/scenario-assets/convertschemacomplete.png)
