## Pre-migration overview

As you prepare for migrating to the cloud, verify that your source environment is supported and that you have address any prerequisites to help ensure a successful migration.

### Migration learnings and best practices from real-world engagements

For additional assistance with completing this migration scenario, please see the following resources, which were developed in support of a real-world migration project engagement.<br>

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
</tbody>
</table>

**Note**: These resources were developed as part of the Data Migration Jumpstart Program (DM Jumpstart), which is sponsored by the Azure Data Group engineering team. The core charter DM Jumpstart is to unblock and accelerate complex modernization and compete data platform migration opportunities to Microsoft’s Azure Data platform. If you think your organization would be interested in participating in the DM Jumpstart program, please contact your account team and ask that they submit a nomination.

### Additional resources

- Be sure to check out the [Azure Total Cost of Ownership (TCO) Calculator](https://aka.ms/azure-tco) to help estimate the cost savings you can realize by migrating your workloads to Azure.
- For a matrix of the Microsoft and third-party services and tools that are available to assist you with various database and data migration scenarios as well as specialty tasks, see the article [Service and tools for data migration](https://docs.microsoft.com/azure/dms/dms-tools-matrix).
- For an overview of the Azure Database Migration Guide and the information it contains, see the video [How to Use the Database Migration Guide](https://azure.microsoft.com/resources/videos/how-to-use-the-azure-database-migration-guide/).
- For a walk through of the phases of the migration process and detail about the specific tools and services recommended to perform assessment and migration, see the video [Overview of the migration journey and the tools/services recommended for performing assessment and migration](https://azure.microsoft.com/resources/videos/overview-of-migration-and-recommended-tools-services/).

## Assess and Convert

By using SQL Server Migration Assistant (SSMA) for Access, you can review database objects and data, assess databases for migration, migrate Access database objects to SQL Server, and then migrate data to SQL Server.

### Steps

To use SSMA for Access to create an assessment, perform the following steps.

1. **Download [SSMA for Access](https://www.microsoft.com/en-us/download/details.aspx?id=54255)**, and then install it.

2. **Assess the source database**.

    a. Under File menu, click "New Project". Provide the details in the New Project dialog
    
    ![Image Alt Text New Project](https://mpbdevcontent.azureedge.net/Images/accessnewprojectsqlazure.png)
    
    b. Click on "Add Databases" and select databases to be added to your new project
    
    ![Image Alt Text Add databases](https://mpbdevcontent.azureedge.net/Images/accessadddb.png)
    
    c. In Access Metadata Explorer, select the database(s) that you want to assess
    
    ![Image Alt Text Select databases](https://mpbdevcontent.azureedge.net/Images/accessselectdb.png)
    
    d. Right-click Databases, and select Create Report
    
     ![Image Alt Text Create Report](https://mpbdevcontent.azureedge.net/Images/accesscreatereport.png)
    
    e. A sample assessment report looks like the below:
    
    ![Image Alt Text Sample Report](https://mpbdevcontent.azureedge.net/Images/accesssamplereport.png)

3. **Converting Access Database Objects**. 

    a. Connect to SQL Azure target database
    
     ![Image Alt Text SQL Server conenction](https://mpbdevcontent.azureedge.net/Images/accessconnecttosqlazure.png)
    
    b. In Access Metadata Explorer, expand access-metabase, and then expand Databases
       
    c. To convert database(s), select the check box next to Databases
      
    d. To convert schemas, right-click Databases and select Convert Schema
    
    ![Image Alt Text SQL Server conenction](https://mpbdevcontent.azureedge.net/Images/accessconvertschema.png)

    Note: You can also convert individual objects. To convert an object, regardless of which objects are selected, right-click the object and select Convert Schema. 

    e. When an object has been converted, it appears bold in Access Metadata Explorer. 
    
    ![Image Alt Text Sample Report](https://mpbdevcontent.azureedge.net/Images/accessconvertcomplete.png)
    
    f. To convert, load, and migrate schemas and data in one step, right-click Databases and select Convert, Load, and Migrate

4. **Review results** in the Output pane and **any errors and warnings** in the Error List pane.