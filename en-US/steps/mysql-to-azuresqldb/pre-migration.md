## Pre-migration overview

As you prepare for migrating to the cloud, verify that your source environment is supported and that you have addressed any prerequisites. This will help to ensure an efficient amd successful migration.

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
<p><a href="https://github.com/Microsoft/DataMigrationTeam/tree/master/Data%20Workload%20Assessment%20Model%20and%20Tool">Data Workload Assessment Model and Tool</a></p>
</td>
<td width="59%">
<p>This tool provides suggested &ldquo;best fit&rdquo; target platforms, cloud readiness, and application/database remediation level for a given workload. It offers simple, one-click calculation and report generation that greatly helps to accelerate large estate assessments by providing and automated and uniform target platform decision process.</p>
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

##  Assess and Convert 

### Steps

To use SSMA for MySQL to create an assessment, perform the following steps.

1. **Download [SSMA for MySQL](https://www.microsoft.com/en-us/download/confirmation.aspx?id=54257)**, and then install it.

2. **Assess the source database** and discover conversion rate and effort to resolve issues.

   a.	Click on the "File" menu and choose "New Project". Provide the project name, a location to save your project and the migration target.

   b.   Select SQL Azure from the “Migrate To” options
    
   c. Click "OK".

   ![New Project](https://mpbdevcontent.azureedge.net/Images/scenario-assets/ssmamysqlnewproject.png)

   d. Connect to the MySQL server by providing the connection details in the "Connect to MySQL" dialog.

   e. Create the conversion report by selecting the MySQL schema in the "MySQL Metadata Explorer" by choosing "Create Report" from the right-click menu options or the menu bar on the top.
   
   ![Create Report](https://mpbdevcontent.azureedge.net/Images/scenario-assets/createreport.png)
   
   f.	This will generate an HTML report with conversion statistics and error/ warnings, if any. Analyze this report to understand conversion issues and its cause.
   
   ![Assessment Report](https://mpbdevcontent.azureedge.net/Images/scenario-assets/assessmentreport.png)
   
   g.	This report can also be accessed from the SSMA projects folder as selected in the first screen. From the example above locate the report.xml file 
   from:
   
   *drive:*\Users\<username>\Documents\SSMAProjects\MySQLMigration\report\report_2016_11_12T02_47_55\
   
   and open it in Excel to get an inventory of MySQL objects and the effort required to perform schema conversions.
   
3. **Perform schema conversion**.

   a. Before you perform schema conversion validate the default datatype mappings or change them based on requirements. You could do so either by navigating to the "Tools" menu and choosing "Project Settings" or you can change type mapping for each table by selecting the table in the "MySQL Metadata Explorer".
   
   ![Type Mappings](https://mpbdevcontent.azureedge.net/Images/scenario-assets/typemappings.png)
   
   b.	Dynamic or ad hoc queries can be added to the "Statements" node by selecting that node and choosing "Add Statement" from the right-click menu options.
   
   c.	For converting and moving the schema to Azure SQL Database, connect to the Azure SQL instance by providing the connection details in the "Connect to Azure SQL Database" dialog. You can choose to connect to an existing database or provide a new name, in which case a database will be created on the target server.
   
   ![Connect to SQL](https://mpbdevcontent.azureedge.net/Images/scenario-assets/connecttosql.png)
   
   d.	Convert the schema by choosing "Convert Schema" from the right-click menu options or the menu bar on the top.
   
   ![Convert Schema](https://mpbdevcontent.azureedge.net/Images/scenario-assets/convertschema.png)
   
   e.	After the schema has converted compare and review the structure of the schema to identify potential problems.
   
   ![Convert Schema](https://mpbdevcontent.azureedge.net/Images/scenario-assets/convertschemacomplete.png)
