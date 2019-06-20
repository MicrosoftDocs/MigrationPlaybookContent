## Pre-migration overview

As you prepare for migrating to the cloud, verify that your source environment is supported and that you have addressed any prerequisites. This will help to ensure an efficient and successful migration.

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
<p><a href="https://github.com/Microsoft/DataMigrationTeam/tree/master/Oracle%20Inventory%20Script%20Artifacts">Oracle Inventory Script Artifacts</a></p>
</td>
<td width="59%">
<p>This asset includes a PL/SQL query that hits Oracle system tables and provides a count of objects by schema type, object type, and status. It also provides a rough estimate of &lsquo;Raw Data&rsquo; in each schema and the sizing of tables in each schema, with results stored in a CSV format.</p>
</td>
</tr>
<tr>
<td width="18%">
<p><a href="https://github.com/Microsoft/DataMigrationTeam/tree/master/SSMA%20Assessment%20Tool">SSMA Assessment Tool</a></p>
</td>
<td width="59%">
<p>This set of resource uses a .csv file as entry (sources.csv in the project folders) to produce the xml files that are needed to run SSMA assessment in console mode. The source.csv is provided by the customer based on an inventory of existing Oracle instances. The output files are <strong>AssessmentReportGeneration_source_1.xml</strong>, <strong>ServersConnectionFile.xml</strong>, and <strong>VariableValueFile.xml</strong>.</p>
</td>
</tr>
<tr>
<td width="18%">
<p><a href="https://aka.ms/dmj-wp-mainframe-optimize">Optimization Guide for Mainframe App/Data recompiled to .NET &amp; SQL Server</a></p>
</td>
<td width="59%">
<p>This guide offers optimization advice for executing point-lookups against SQL Server from .NET as efficiently as possible. Customers wishing to migrate from mainframe databases to SQL Server may desire to migrate existing mainframe-optimized design patterns, especially when using 3rd party tools (such as Raincode Compiler) to automatically migrate mainframe code (COBOL/JCL, etc.) to T-SQL and C# .NET.</p>
</td>
</tr>
<tr>
<td width="18%">
<p><a href="https://aka.ms/dmj-wp-oracle-sql-handbook">Oracle to SQL Server Migration Handbook</a></p>
</td>
<td width="59%">
<p>This document focuses on the tasks associated with migrating an Oracle database to the latest version of SQL Serverbase. If the migration requires changes to features/functionality, then the possible impact of each change on the applications that use the database must be considered carefully.</p>
</td>
</tr>
<tr>
<td width="18%">
<p><a href="https://aka.ms/dmj-wp-ssma-oracle-errors">SSMA for Oracle Common Errors and how to fix them</a></p>
</td>
<td width="59%">
<p>With Oracle, you can assign a non-scalar condition in the WHERE clause. However, SQL Server doesn&rsquo;t support this type of condition. As a result, SQL Server Migration Assistant (SSMA) for Oracle doesn&rsquo;t&nbsp;convert queries with a non-scalar condition in the WHERE clause, instead generating an error&nbsp;O2SS0001. This white paper provides more details on the issue and ways to resolve it.</p>
</td>
</tr>
<tr>
<td width="18%">
<p><a href="https://aka.ms/dmj-wp-oracle12c-linux">Setting up Oracle 12c Enterprise and Getting It Working by Using the Azure Marketplace Template</a></p>
</td>
<td width="59%">
<p>This white paper provides a step-by-step walkthrough of setting up and implementing Oracle 12c Enterprise by using the Azure Marketplace Template.</p>
</td>
</tr>
</tbody>
</table>

**Note**: These resources were developed as part of the Data Migration Jumpstart Program (DM Jumpstart), which is sponsored by the Azure Data Group engineering team. The core charter DM Jumpstart is to unblock and accelerate complex modernization and compete data platform migration opportunities to Microsoft’s Azure Data platform. If you think your organization would be interested in participating in the DM Jumpstart program, please contact your account team and ask that they submit a nomination.

### Additional resources

- Be sure to check out the [Azure Total Cost of Ownership (TCO) Calculator (Preview)](https://aka.ms/azure-tco) to help estimate the cost savings you can realize by migrating your workloads to Azure.
- For an overview of the Azure Database Migration Guide and the information it contains, see the video [How to Use the Database Migration Guide](https://azure.microsoft.com/resources/videos/how-to-use-the-azure-database-migration-guide/).
- For a walk through of the phases of the migration process and detail about the specific tools and services recommended to perform assessment and migration, see the video [Overview of the migration journey and the tools/services recommended for performing assessment and migration](https://azure.microsoft.com/resources/videos/overview-of-migration-and-recommended-tools-services/).

## Discover


The goal of the Discover phase is to identify existing data sources and details about the features that are being used to get a better understanding of and plan for the migration. This process involves scanning the network to identify all your organization’s Oracle instances together with the version and features in use.

### Steps

To use the MAP Toolkit to perform an inventory scan, perform the following steps.

1. **Download the [MAP Toolkit](http://go.microsoft.com/fwlink/?LinkID=316883)**, and then install it.

2. **Run the MAP toolkit**.

    a. Open the MAP toolkit, and then on the left pane, select **Database**.
    
    You will be on the following screen:
    
    ![MAP Overview](https://mpbdevcontent.azureedge.net/Images/mapoverview.png)
    
    b. Select **Create/Select database**.
    
    ![MAP Create/Select DB](https://mpbdevcontent.azureedge.net/Images/mapselectdb.png)
     
    c. Ensure that **Create an inventory database** is selected, enter a name for the database, a brief description, and then select **OK**.
    
    ![MAP Create/Select DB Overview](https://mpbdevcontent.azureedge.net/Images/mapselectdboverview.png)
    
    The next step is to collect data from the database created.
    
    d. Select **Collect inventory data**.
    
    ![MAP Collect Inventory Data](https://mpbdevcontent.azureedge.net/Images/maporacleoverview.png)
    
    e. In the Inventory and Assessment Wizard, select **Oracle**, and then select **Next**.
    
    ![MAP Inventory and Assessment Wizard](https://mpbdevcontent.azureedge.net/Images/mapinventorywizard_oracle.png)
    
    f. Select the best method option to search the computers on which Microsoft Products are hosted, and then select **Next**.
    
    ![MAP Inventory and Assessment Wizard Discovery Methods](https://mpbdevcontent.azureedge.net/Images/mapdiscoverymethods.png)
    
    g. Enter credentianls or create new credentials for the systems that you want to explore, and then select **Next**.
    
    ![MAP Inventory and Assessment Wizard Discovery Credentials](https://mpbdevcontent.azureedge.net/Images/mapdiscoverycreds.png)
    
    h. Set the order of the credentials.
    
    ![MAP Inventory and Assessment Wizard Discovery Credentials Order](https://mpbdevcontent.azureedge.net/Images/mapdiscoverycredsorder2.png)
    
    Now, you need to specify the credentials for each computer you want to discover. You can use unique credentials for every computer/machine, or you can choose to use the **All Computer Credentials** list.
    
    i. After setting up the credentials, select **Save**, and then select **Next**.
    
    ![MAP Inventory and Assessment Wizard Discovery Credentials](https://mpbdevcontent.azureedge.net/Images/mapdiscoverycredsindividual.png)
    
    j. Verify your selection summary, and then select **Finish**.
    
    ![MAP Inventory and Assessment Wizard Summary](https://mpbdevcontent.azureedge.net/Images/mapdiscoverysummary.png)
    
    k. Wait for a few minutes (depending on the number of databases) for the Data Collection summary report.
    
    ![MAP Inventory and Assessment Wizard Summary](https://mpbdevcontent.azureedge.net/Images/mapdatacollectionsummary.png)
    
    l. Select **Close**.
    
    The Main window of the tool appears, showing a summary of the Database Discovery completed so far.
    
 3. **Report generation and data collection**.
    
    On top right corner of the tool, an **Options** page appears, which you can use to generate a report about the Oracle Assessment and the Database Details.
       
    a. Select both options (one by one) to generate the report.
    
    This will take a couple of seconds to a few minutes depending upon the size of the inventory comlpeted during discovery.
    
    ![MAP Report Generation](https://mpbdevcontent.azureedge.net/Images/mapexcelreportdone.png)

## Assess and Convert

After identifying the data sources, the next step is to assess the Oracle instance(s) migrating to SQL Server database(s) so that you understand the gaps between the two.

By using the SQL Server Migration Assistant (SSMA) for Oracle, you can review database objects and data, assess databases for migration, migrate database objects to SQL Server, and then migrate data to SQL Server. 

### Steps

To use SSMA for Oracle to create an assessment, perform the following steps.

1. **Download [SSMA](https://www.microsoft.com/en-us/download/details.aspx?id=54258)**, and then install it.

2. Create a new **Assessment project** to discover the conversion rate and effort to resolve any issues.

   a. On **File** menu, select **New Project**, specify the project name, a location to save your project, and the migration target.
   
   _Selecting the migration target is important to accurately assess the conversion rate and effort._
  
   b. Select **OK**.

   ![Image Alt Text New Project](https://mpbdevcontent.azureedge.net/Images/newproject.png)

   c. Select **Connect to Oracle**, provide the connection details, and then select **Connect**.
   
   ![Image Alt Text Connect to Oracle](https://mpbdevcontent.azureedge.net/Images/connecttooracle.png)
   
   d. In the **Oracle Metadata Explorer**, select the Oracle schema, and then select **Create Report** to create the conversion report.
   
   ![Image Alt Text Create Report](https://mpbdevcontent.azureedge.net/Images/createreport.png)
   
    This will generate an HTML report with conversion statistics and error/warnings, if any.
     
   e. Analyze this report to understand any conversion issues and their cause.
   
   ![Image Alt Text Assessment Report](https://mpbdevcontent.azureedge.net/Images/assessmentreport.png)
   
   You can also access this report from the SSMA projects folder as selected in the first screen.
   
   f. From the example above locate the report.xml file from: 
   
   *drive:*\Users\<username>\Documents\SSMAProjects\MyOracleMigration\report\report_2016_11_12T02_47_55\
   
   and then open it in Excel to get an inventory of Oracle objects and the effort required to perform schema conversions.
   
3. **Perform schema conversion**.

   a. Before you perform schema conversion, validate the default datatype mappings or change them based on requirements.
   
   You could do this either by navigating to the **Tools** menu and selecting **Project Settings** or by changing the type mapping for each table by selecting the table in the **Oracle Metadata Explorer**.
   
   ![Image Alt Text Type Mappings](https://mpbdevcontent.azureedge.net/Images/typemappings.png)
   
   You can add dynamic or ad hoc queries to the **Statements** node by selecting that node and then selecting **Add Statement** on the right-click menu.
   
   b. To convert and move the schema to SQL Server, connect to the SQL server instance by providing the connection details in the **Connect to SQL Server** dialog box.
   
   You can choose to connect to an existing database or provide a new name, in which case a database will be created on the target server.
   
   ![Image Alt Text Connect to SQL](https://mpbdevcontent.azureedge.net/Images/connecttosql.png)
   
   c.	Convert the schema by selecting **Convert Schema** from the right-click menu or the menu bar on the top.
   
   ![Image Alt Text Convert Schema](https://mpbdevcontent.azureedge.net/Images/convertschema.png)
   
   d.	After schema conversion, compare and review the structure of the schema to identify potential problems.
   
   ![Image Alt Text Convert Schema](https://mpbdevcontent.azureedge.net/Images/convertschemacomplete.png)