## Pre-migration overview

As you prepare for upgrading your SQL Server database to a later version of SQL Server, consider the versions of SQL Server that are supported and to address any prerequisites. This will help to ensure an efficient and successful migration.

### Supported upgrade technologies

This section describes all supported scenarios and options for an upgrade from and older version of SQL Server to a newer version of SQL Server, current as of March 2019.

Supported source and target versions are shown in the following table.

<br>
<table style="width: 650px;">
<thead>
<tr>
<td style="width: 325px; vertical-align: middle;">
<p><strong>&nbsp;SQL Server source versions</strong></p>
</td>
<td style="width: 325px; vertical-align: middle;">
<p><strong>&nbsp;SQL Server target versions</strong></p>
</td>
</tr>
</thead>
<tbody>
<tr>
<td style="width: 325px; vertical-align: top;">
<ul>
<li>SQL Server 2005</li>
<li>SQL Server 2008, SQL Server 2008 R2</li>
<li>SQL Server 2012</li>
<li>SQL Server 2014</li>
<li>SQL Server 2016</li>
</ul>
</td>
<td style="width: 325px; vertical-align: top;">
<ul>
<li>SQL Server 2014</li>
<li>SQL Server 2016</li>
<li>SQL Server 2017 on Linux</li>
<li>SQL Server 2017 on Windows</li>
</ul>
</td>
</tr>
</tbody>
</table>

The following data migration options are discussed:
*	Backup and restore
*	Transactional replication
*	Always On availability groups
*	Data Migration tool set (Azure Database Migration Service [Azure DMS] and Data Migration Assistant [DMA])
*	Database mirroring
*	Log shipping
*	Bulk load

#### Upgrading from SQL Server 2005
When upgrading from SQL Server 2005, the following migration options are supported.

<br>
<table width="100%">
<thead>
<tr>
<td width="131">
<p><strong>Target version</strong></p>
</td>
<td width="539">
<p><strong>Database migration options</strong></p>
</td>
</tr>
</thead>
<tbody>
<tr>
<td width="131">
<p>SQL Server 2017</p>
</td>
<td width="539">
<ul>
<li><u>Migration tools</u>: Migration is supported through <a href="https://aka.ms/dma">Data Migration Assistant</a> (DMA).</li>
<li>Backup and restore: A backup taken on SQL Server 2005 can be restored to SQL Server 2017.</li>
<li><u>Bulk load</u>: Tables can be bulk copied from SQL Server 2005 to SQL Server 2017.</li>
</ul>
</td>
</tr>
<tr>
<td width="131">
<p>SQL Server 2016</p>
</td>
<td width="539">
<ul>
<li><u>Migration tools</u>: Migration is supported through <a href="https://aka.ms/dam">DMA</a>.</li>
<li><u>Backup and restore</u>: A backup taken on SQL Server 2005 can be restored to SQL Server 2016.</li>
<li><u>Bulk load</u>: Tables can be bulk copied from SQL Server 2005 to SQL Server 2016.</li>
</ul>
</td>
</tr>
<tr>
<td width="131">
<p>SQL Server 2014</p>
</td>
<td width="539">
<ul>
<li><u>Migration tools</u>: Migration is supported through <a href="https://aka.ms/dam">DMA</a>.</li>
<li><u>Backup and restore</u>: A backup taken on SQL Server 2005 can be restored to SQL Server 2014.</li>
<li><u>Bulk load</u>: Tables can be bulk copied from SQL Server 2005 to SQL Server 2014.</li>
</ul>
</td>
</tr>
</tbody>
</table>

#### Upgrading from SQL Server 2008 or SQL Server 2008 R2
When upgrading from SQL Server 2008 or SQL Server 2008 R2, the following migration options are supported.

<br>
<table width="100%">
<thead>
<tr>
<td width="131">
<p><strong>Target version</strong></p>
</td>
<td width="539">
<p><strong>Database migration options</strong></p>
</td>
</tr>
</thead>
<tbody>
<tr>
<td width="131">
<p>SQL Server 2017</p>
</td>
<td width="539">
<ul>
<li><u>Migration tools</u>: Migration is supported through <a href="https://aka.ms/dma">Data Migration Assistant</a> (DMA).</li>
<li><u>Backup and restore</u>: A backup taken on SQL Server 2008 or SQL Server 2008 R2 can be restored to SQL Server 2017.</li>
<li><u>Database mirroring</u>: Database mirroring is supported if principal is running SQL Server 2008 SP3 or later, or SQL Server 2008 R2 SP2 or later, and mirror is running SQL Server 2017. If a failover, either automatic or manual, happens such that SQL Server 2017 instance becomes principal, SQL Server 2008 or SQL Server 2008 R2 instance becomes mirror and will NOT receive changes from principal.</li>
<li><u>Log shipping</u>: Log shipping is supported if primary is running SQL Server 2008 SP3 or later, or SQL Server 2008 R2 SP2 or later, and secondary is running SQL Server 2017. If a failover, either automatic or manual, happens such that SQL Server 2017 instance becomes primary, SQL Server 2008 or SQL Server 2008 R2 instance becomes secondary and will NOT receive changes from primary.</li>
<li><u>Bulk load</u>: Tables can be bulk copied from SQL Server 2008 or SQL Server 2008 R2 to SQL Server 2017.</li>
</ul>
</td>
</tr>
<tr>
<td width="131">
<p>SQL Server 2016</p>
</td>
<td width="539">
<ul>
<li><u>Migration tools</u>: Migration is supported through <a href="https://aka.ms/dam">DMA</a>.</li>
<li><u>Backup and restore</u>: A backup taken on SQL Server 2008 or SQL Server 2008 R2 can be restored to SQL Server 2016.</li>
<li><u>Database mirroring</u>: Database mirroring is supported if principal is running SQL Server 2008 SP3 or later, or SQL Server 2008 R2 SP2 or later, and mirror is running SQL Server 2016. If a failover, either automatic or manual, happens such that SQL Server 2016 instance becomes principal, SQL Server 2008 or SQL Server 2008 R2 instance becomes mirror and will NOT receive changes from principal.</li>
<li><u>Log shipping</u>: Log shipping is supported if primary is running SQL Server 2008 SP3 or later, or SQL Server 2008 R2 SP2 or later, and secondary is running SQL Server 2016. If a failover, either automatic or manual, happens such that SQL Server 2016 instance becomes primary, SQL Server 2008 or SQL Server 2008 R2 instance becomes secondary and will NOT receive changes from primary.</li>
<li><u>Bulk load</u>: Tables can be bulk copied from SQL Server 2008 or SQL Server 2008 R2 to SQL Server 2016.</li>
</ul>
</td>
</tr>
<tr>
<td width="131">
<p>SQL Server 2014</p>
</td>
<td width="539">
<ul>
<li><u>Migration tools</u>: Migration is supported through <a href="https://aka.ms/dam">DMA</a>.</li>
<li><u>Backup and restore</u>: A backup taken on SQL Server 2008 or SQL Server 2008 R2 can be restored to SQL Server 2014.</li>
<li><u>Transactional replication</u>: SQL Server replication from SQL Server 2008/2008R2 to SQL Server is supported. Replication upgrade options are outlined in detail in the blog&nbsp;<a href="https://blogs.msdn.microsoft.com/sql_server_team/upgrading-a-replication-topology-to-sql-server-2016/">here</a>.</li>
<li><u>Database mirroring</u>: Database mirroring is supported if principal is running SQL Server 2008 SP3 or later, or SQL Server 2008 R2 SP2 or later, and mirror is running SQL Server 2014. If a failover, either automatic or manual, happens such that SQL Server 2014 instance becomes principal, SQL Server 2008 or SQL Server 2008 R2 instance becomes mirror and will NOT receive changes from principal.</li>
<li><u>Log shipping</u>: Log shipping is supported if primary is running SQL Server 2008 SP3 or later, or SQL Server 2008 R2 SP2 or later, and secondary is running SQL Server 2014. If a failover, either automatic or manual, happens such that SQL Server 2014 instance becomes primary, SQL Server 2008 or SQL Server 2008 R2 instance becomes secondary and will NOT receive changes from primary.</li>
<li><u>Bulk load</u>: Tables can be bulk copied from SQL Server 2008 or SQL Server 2008 R2 to SQL Server 2014.</li>
</ul>
</td>
</tr>
</tbody>
</table>

#### Upgrading from SQL Server 2012
When upgrading from SQL Server 2012, the following migration options are supported.

<br>
<table width="100%">
<thead>
<tr>
<td width="131">
<p><strong>Target version</strong></p>
</td>
<td width="539">
<p><strong>Database migration options</strong></p>
</td>
</tr>
</thead>
<tbody>
<tr>
<td width="131">
<p>SQL Server 2017</p>
</td>
<td width="539">
<ul>
<li><u>Migration tools</u>: Migration is supported through <a href="https://aka.ms/dma">Data Migration Assistant</a> (DMA).</li>
<li><u>Backup and restore</u>: A backup taken on SQL Server 2012 can be restored to SQL Server 2017.</li>
<li><u>Transactional replication</u>: SQL Server transactional replication from SQL Server 2012 to SQL Server 2017 is supported.</li>
<li><u>Availability group</u>: Always On availability groups are supported if primary replica is running SQL Server 2012 SP2 or later and secondary replicas are running SQL Server 2017. If a failover, either automatic or manual, happens such that a SQL Server 2017 instance becomes primary, SQL Server 2012 instance becomes secondary and will NOT be able to receive changes from primary.</li>
<li><u>Database mirroring</u>: Database mirroring is supported if principal is running SQL Server 2012 SP1 or later and mirror is running SQL Server 2017. If a failover, either automatic or manual, happens such that SQL Server 2017 instance becomes principal, SQL Server 2012 instance becomes mirror and will NOT receive changes from principal.</li>
<li><u>Log shipping</u>: Log shipping is supported if primary is running SQL Server 2012 SP1 or later and secondary is running SQL Server 2017. If a failover, either automatic or manual, happens such that SQL Server 2017 instance becomes primary, SQL Server 2012 instance becomes secondary and will NOT receive changes from primary.</li>
<li><u>Bulk load</u>: Tables can be bulk copied from SQL Server 2012 to SQL Server 2017.</li>
</ul>
</td>
</tr>
<tr>
<td width="131">
<p>SQL Server 2016</p>
</td>
<td width="539">
<ul>
<li><u>Migration tools</u>: Migration is supported through <a href="https://aka.ms/dam">DMA</a>.</li>
<li><u>Backup and restore</u>: A backup taken on SQL Server 2012 can be restored to SQL Server 2016.</li>
<li><u>Transactional replication</u>: SQL Server transactional replication from SQL Server 2012 to SQL Server 2016 is supported.</li>
<li><u>Availability group</u>: Always On availability groups are supported if primary replica is running SQL Server 2012 SP2 or later and secondary replicas are running SQL Server 2016. If a failover, either automatic or manual, happens such that a SQL Server 2016 instance becomes primary, SQL Server 2012 instance becomes secondary and will NOT be able to receive changes from primary.</li>
<li><u>Database mirroring</u>: Database mirroring is supported if principal is running SQL Server 2012 SP1 or later and mirror is running SQL Server 2016. If a failover, either automatic or manual, happens such that SQL Server 2016 instance becomes principal, SQL Server 2012 instance becomes mirror and will NOT receive changes from principal.</li>
<li><u>Log shipping</u>: Log shipping is supported if primary is running SQL Server 2012 SP1 or later and secondary is running SQL Server 2016. If a failover, either automatic or manual, happens such that SQL Server 2016 instance becomes primary, SQL Server 2012 instance becomes secondary and will NOT receive changes from primary.</li>
<li><u>Bulk load</u>: Tables can be bulk copied from SQL Server 2012 to SQL Server 2016.</li>
</ul>
</td>
</tr>
<tr>
<td width="131">
<p>SQL Server 2014</p>
</td>
<td width="539">
<ul>
<li><u>Migration tools</u>: Migration is supported through <a href="https://aka.ms/dam">DMA</a>.</li>
<li><u>Backup and restore</u>: A backup taken on SQL Server 2012 can be restored to SQL Server 2014.</li>
<li><u>Transactional replication</u>: SQL Server transactional replication from SQL Server 2012 to SQL Server 2014 is supported.</li>
<li><u>Availability group</u>: Always On availability groups are supported if primary replica is running SQL Server 2012 SP1 or later and secondary replicas are running SQL Server 2014. If a failover, either automatic or manual, happens such that a SQL Server 2014 instance becomes primary, SQL Server 2012 instance becomes secondary and will NOT be able to receive changes from primary.</li>
<li><u>Database mirroring</u>: Database mirroring is supported if principal is running SQL Server 2012 SP1 or later and mirror is running SQL Server 2014. If a failover, either automatic or manual, happens such that SQL Server 2014 instance becomes principal, SQL Server 2012 instance becomes mirror and will NOT receive changes from principal.</li>
<li><u>Log shipping</u>: Log shipping is supported if primary is running SQL Server 2012 SP1 or later and secondary is running SQL Server 2014. If a failover, either automatic or manual, happens such that SQL Server 2014 instance becomes primary, SQL Server 2012 instance becomes secondary and will NOT receive changes from primary.</li>
<li><u>Bulk load</u>: Tables can be bulk copied from SQL Server 2012 to SQL Server 2014.</li>
</ul>
</td>
</tr>
</tbody>
</table>

#### Upgrading from SQL Server 2014
When upgrading from SQL Server 2014, the following migration options are supported.

<br>
<table width="100%">
<thead>
<tr>
<td width="131">
<p><strong>Target version</strong></p>
</td>
<td width="539">
<p><strong>Database migration options</strong></p>
</td>
</tr>
</thead>
<tbody>
<tr>
<td width="131">
<p>SQL Server 2017</p>
</td>
<td width="539">
<ul>
<li><u>Migration tools</u>: Migration is supported through <a href="https://aka.ms/dma">Data Migration Assistant</a> (DMA).</li>
<li><u>Backup and restore</u>: A backup taken on SQL Server 2014 can be restored to SQL Server 2017.</li>
<li><u>Transactional replication</u>: SQL Server transactional replication from SQL Server 2014 to SQL Server 2017 is supported.</li>
<li><u>Availability group</u>: Always On availability groups are supported if primary replica is running SQL Server 2014 and secondary replicas are running SQL Server 2017. If a failover, either automatic or manual, happens such that a SQL Server 2017 instance becomes primary, SQL Server 2014 instance becomes secondary and will NOT be able to receive changes from primary.</li>
<li><u>Database mirroring</u>: Database mirroring is supported if principal is running SQL Server 2014 and mirror is running SQL Server 2017. If a failover, either automatic or manual, happens such that SQL Server 2017 instance becomes principal, SQL Server 2014 instance becomes mirror and will NOT receive changes from principal.</li>
<li><u>Log shipping</u>: Log shipping is supported if primary is running SQL Server 2014 and secondary is running SQL Server 2017. If a failover, either automatic or manual, happens such that SQL Server 2017 instance becomes primary, SQL Server 2014 instance becomes secondary and will NOT receive changes from primary.</li>
<li><u>Bulk load</u>: Tables can be bulk copied from SQL Server 2014 to SQL Server 2017.</li>
</ul>
</td>
</tr>
<tr>
<td width="131">
<p>SQL Server 2016</p>
</td>
<td width="539">
<ul>
<li><u>Migration tools</u>: Migration is supported through <a href="https://aka.ms/dam">DMA</a>.</li>
<li>Backup and restore: A backup taken on SQL Server 2014 can be restored to SQL Server 2016.</li>
<li>Transactional replication: SQL Server transactional replication from SQL Server 2014 to SQL Server 2016 is supported.</li>
<li><u>Availability group</u>: Always On availability groups are supported if primary replica is running SQL Server 2014 and secondary replicas are running SQL Server 2016. If a failover, either automatic or manual, happens such that a SQL Server 2016 instance becomes primary, SQL Server 2014 instance becomes secondary and will NOT be able to receive changes from primary.</li>
<li><u>Database mirroring</u>: Database mirroring is supported if principal is running SQL Server 2014 and mirror is running SQL Server 2016. If a failover, either automatic or manual, happens such that SQL Server 2016 instance becomes principal, SQL Server 2014 instance becomes mirror and will NOT receive changes from principal.</li>
<li><u>Log shipping</u>: Log shipping is supported if primary is running SQL Server 2014 and secondary is running SQL Server 2016. If a failover, either automatic or manual, happens such that SQL Server 2016 instance becomes primary, SQL Server 2014 instance becomes secondary and will NOT receive changes from primary.</li>
<li><u>Bulk load</u>: Tables can be bulk copied from SQL Server 2014 to SQL Server 2016.</li>
</ul>
</td>
</tr>
</tbody>
</table>

#### Upgrading from SQL Server 2016
When upgrading from SQL Server 2016, the following migration options are supported.

<br>
<table width="100%">
<thead>
<tr>
<td width="131">
<p><strong>Target version</strong></p>
</td>
<td width="539">
<p><strong>Database migration options</strong></p>
</td>
</tr>
</thead>
<tbody>
<tr>
<td width="131">
<p>SQL Server 2017</p>
</td>
<td width="539">
<ul>
<li><u>Migration tools</u>: Migration is supported through <a href="https://aka.ms/dma">Data Migration Assistant</a> (DMA).</li>
<li><u>Backup and restore</u>: A backup taken on SQL Server 2016 can be restored to SQL Server 2017.</li>
<li><u>Transactional replication</u>: SQL Server transactional replication from SQL Server 2016 to SQL Server 2017 is supported.</li>
<li><u>Availability group</u>: Always On availability groups are supported if primary replica is running SQL Server 2016 and secondary replicas are running SQL Server 2017. If a failover, either automatic or manual, happens such that a SQL Server 2017 instance becomes primary, the SQL Server 2016 instance becomes secondary and will NOT be able to receive changes from primary.</li>
<li><u>Database mirroring</u>: Database mirroring is supported if principal is running SQL Server 2016 and mirror is running SQL Server 2017. If a failover, either automatic or manual, happens such that a SQL Server 2017 instance becomes principal, the SQL Server 2016 instance becomes a mirror and will NOT receive changes from principal.</li>
<li><u>Log shipping</u>: Log shipping is supported if primary is running SQL Server 2016 and secondary is running SQL Server 2017. If a failover, either automatic or manual, happens such that SQL Server 2017 instance becomes primary, the SQL Server 2016 instance becomes secondary and will NOT receive changes from primary.</li>
<li><u>Bulk load</u>: Tables can be bulk copied from SQL Server 2016 to SQL Server 2017.</li>
</ul>
</td>
</tr>
</tbody>
</table>

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

- For an overview of the Azure Database Migration Guide and the information it contains, see the video [How to Use the Database Migration Guide](https://azure.microsoft.com/resources/videos/how-to-use-the-azure-database-migration-guide/).
- For a walk through of the phases of the migration process and detail about the specific tools and services recommended to perform assessment and migration, see the video [Overview of the migration journey and the tools/services recommended for performing assessment and migration](https://azure.microsoft.com/resources/videos/overview-of-migration-and-recommended-tools-services/).

### Prerequisites

Before beginning your migration project, it is important to address the associated prerequisites. To prepare for the migration, download and install the:

* Latest version of the [MAP Toolkit](http://go.microsoft.com/fwlink/?LinkID=316883).
* [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) v3.3 or later.
* Latest version of the [Database Experimentation Assistant](https://www.microsoft.com/en-us/download/details.aspx?id=54090).

## Discover

The goal of the Discover phase is to identify existing data sources and details about the features that are being used to get a better understanding of and plan for the migration. This process involves scanning the network to identify all your organization’s SQL instances together with the version and features in use.

To use the MAP Toolkit to perform an inventory scan, perform the following steps.

### Steps

1. Download the [MAP Toolkit](http://go.microsoft.com/fwlink/?LinkID=316883), and then install it.

2. Run the MAP Toolkit.

    a. Open the MAP Toolkit, and then on the left pane, select **Database**.
    
    You will be on the following screen:
    
    ![MAP Overview](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapoverview.png)
    
    b. Select **Create/Select database**.
    
    ![MAP Create/Select DB](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapselectdb.png)
     
    c. Ensure that **Create an inventory database** is selected, enter a name for the database, a brief description, and then select **OK**.
    
    ![MAP Create/Select DB Overview](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapselectdboverview.png)
    
    The next step is to collect data from the database created.

    d. Select **Collect inventory data**.
    
    ![MAP Collect Inventory Data](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapcollectinventorydata.png)
    
    e. In the Inventory and Assessment Wizard, select **SQL Server** and **SQL Server with Database Details**, and then select **Next**.
    
    ![MAP Inventory and Assessment Wizard](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapinventorywizard.png)
    
    f. Select the best method option to search the computers on which Microsoft Products are hosted, and then select **Next**.
    
    ![MAP Inventory and Assessment Wizard Discovery Methods](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapdiscoverymethods.png)
    
    g. Enter credentials or create new credentials for the systems that you want to explore, and then select **Next**.
    
   ![MAP Inventory and Assessment Wizard Discovery Credentials](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapdiscoverycreds.png)
    
    h. Set the order of the credentials, and then select **Next**.
               
    ![MAP Inventory and Assessment Wizard Discovery Credentials Order](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapdiscoverycredsorder.png)
    
    Now, you need to specify the credentials for each computer that you want to discover. You can use unique credentials for each computer/machine, or you can choose to use the **All Computer Credentials** list.
    
    i. After setting up the credentials, select **Save**, and then select **Next**.
    
    ![MAP Inventory and Assessment Wizard Discovery Credentials](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapdiscoverycredsindividual.png)
    
    j. Verify your selection summary, and then select **Finish**.
    
    ![MAP Inventory and Assessment Wizard Summary](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapdiscoverysummary.png)
    
    k. Wait for a few minutes (depending on the number of databases) for the Data Collection summary report.
    
    ![MAP Inventory and Assessment Wizard Summary](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapdatacollectionsummary.png)
    
    l. Select **Close**.
    
    The Main window of the tool appears, showing a summary of the Database Discovery completed so far.
    
 3. Report generation and data collection.
    
    On the top-right corner of the tool, an **Options** page appears, which you can use to generate report about the SQL Server Assessment and the Database Details.
    
    ![MAP Report Generation](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapexcelreport.png)
    
    a. Select both options (one by one) to generate the report.
    
    This will take a couple of seconds to a few minutes depending on the size of the inventory completed during discovery.
    
    ![MAP Report Generation](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapexcelreportdone.png)

## Assess

After identifying the data sources, the next step is to assess the on-premises SQL Server instance(s) upgrading to a later version of SQL Server so that you understand the gaps between the source and target instances. Use the Data Migration Assistant (DMA) to assess your source database before upgrading your SQL Server instance.

### Steps

To use DMA to create an assessment, perform the following steps.

1. Download the [DMA tool](https://www.microsoft.com/en-us/download/details.aspx?id=53595), and then install it.

2. Create a **New Assessment** project.

    a. Select the New (+) icon, select the **Assessment** project type, specify a project name, select **SQL Server** as the source and target, and then select **Create**.
    
    ![New Assessment](https://mpbdevcontent.azureedge.net/Images/scenario-assets/dmanewproject.bmp)    
    
    b. Select the target SQL Server version that you plan to migrate to and against which you need to run an assessment, select one or both of the assessment report types (**Compatibility Issues** and **New features’ recommendation**), and then select **Next**.
    
    ![Report Types](https://mpbdevcontent.azureedge.net/Images/scenario-assets/dmaassessment.bmp)   
    
    c. In the **Connect to a server** fly-out, specify the name of the SQL Server instance to connect to, specify the Authentication type and Connection properties, and then select **Connect**.
    
    d. In the **Add Sources** fly-out, select the database(s) you that want to assess, and then select **Add**.
            
    ![Add databases](https://mpbdevcontent.azureedge.net/Images/scenario-assets/dmaadddb.bmp)   
    
    e. Select **Start Assessment**.
    
    Now wait for the assessment results; the duration of the assessment depends on the number of databases added and the schema size of each database. Results will be displayed per database as soon as they are available.
    
    f. Select the database that has completed assessment, and then switch between **Compatibility issues** and **Feature recommendations** by using the switcher.
    
    ![Assessment results](https://mpbdevcontent.azureedge.net/Images/scenario-assets/dmaassessmentresults.bmp)  
    
    g. Review the compatibility issues by analyzing the impacted object and its details for every issue identified under **Breaking changes**, **Behavior changes**, and **Deprecated features**.
    
    h. Review feature recommendations across the **Performance**, **Storage**, and **Security** areas.
    
    Feature recommendations cover a variety of features such as In-Memory OLTP and Columnstore, Stretch Database, Always Encrypted (AE), Dynamic Data Masking (DDM), and Transparent Data Encryption (TDE). 
    
3. Review assessment results.

    a. After all database assessments are complete, select **Export report** to export the results to either a JSON or CSV file for analyzing the data at your own convenience.

## Convert

After assessing the source database instance(s) you are migrating, for heterogenous migrations, you need to convert the schema to work in the target environment. Since upgrading to a newer version of SQL Server would be considered a homogeneous migration, the Convert phase is unnecessary.
