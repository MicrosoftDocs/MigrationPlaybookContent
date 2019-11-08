## Pre-migration overview

After verifying that your source environment is supported and ensuring that you have addressed any prerequisites, you are ready to start the Pre-migration stage. This part of the process involves conducting an inventory of the databases that you need to migrate, assessing those databases for potential migration issues or blockers, and then resolving any items you might have uncovered.

## Assess and Convert

After identifying the data sources, the next step is to assess the Oracle instance(s) migrating to Azure SQL Database database(s) so that you understand the gaps between the two.

By using the SQL Server Migration Assistant (SSMA) for Oracle, you can review database objects and data, assess databases for migration, migrate database objects to SQL Server, and then migrate data to SQL Server. 

To use SSMA for Oracle to create an assessment, perform the following steps.

### Steps

1. **Download [SSMA](https://www.microsoft.com/en-us/download/details.aspx?id=54258)**, and then install it.

2. **Assess the source database** and discover conversion rate and effort to resolve issues.

   a.	Click on the "File" menu and choose "New Project". Provide the project name, a location to save your project and the migration target.

   b.   Select Azure SQL Database from the “Migrate To” options
    
   c. Click "OK".

   ![New Project](https://mpbdevcontent.azureedge.net/Images/scenario-assets/newproject.png)

   d. Connect to the Oracle server by providing the connection details in the "Connect to Oracle" dialog.
   
   ![Connect to Oracle](https://mpbdevcontent.azureedge.net/Images/scenario-assets/connecttooracle.png)
   
   e.	Create the conversion report by selecting the Oracle schema in the "Oracle Metadata Explorer" by choosing "Create Report" from the right-click menu options or the menu bar on the top.
   
   ![Create Report](https://mpbdevcontent.azureedge.net/Images/scenario-assets/createreport.png)
   
   f.	This will generate an HTML report with conversion statistics and error/ warnings, if any. Analyze this report to understand conversion issues and its cause.
   
   ![Assessment Report](https://mpbdevcontent.azureedge.net/Images/scenario-assets/assessmentreport.png)
   
   g.	This report can also be accessed from the SSMA projects folder as selected in the first screen. From the example above locate the report.xml file 
   from:
   
   *drive*:\Users\<username>\Documents\SSMAProjects\MyOracleMigration\report\report_2016_11_12T02_47_55\
   
   and open it in Excel to get an inventory of oracle objects and the effort required to perform schema conversions.
   
3. **Perform schema conversion**.

   a. Before you perform schema conversion validate the default datatype mappings or change them based on requirements. You could do so either by navigating to the "Tools" menu and choosing "Project Settings" or you can change type mapping for each table by selecting the table in the "Oracle Metadata Explorer".
   
   ![Image Alt Text Type Mappings](https://mpbdevcontent.azureedge.net/Images/scenario-assets/typemappings.png)
   
   b.	Dynamic or ad hoc queries can be added to the "Statements" node by selecting that node and choosing "Add Statement" from the right-click menu options.
   
   c.	For converting and moving the schema to Azure SQL Database, connect to the SQL instance by providing the connection details in the "Connect to Azure SQL" dialog. You can choose to connect to an existing database or provide a new name, in which case a database will be created on the target server.
   
   ![Image Alt Text Connect to SQL](https://mpbdevcontent.azureedge.net/Images/scenario-assets/connecttosql.png)
   
   d.	Convert the schema by choosing "Convert Schema" from the right-click menu options or the menu bar on the top.
   
   ![Image Alt Text Convert Schema](https://mpbdevcontent.azureedge.net/Images/scenario-assets/convertschema.png)
   
   e.	After the schema has converted compare and review the structure of the schema to identify potential problems.
   
   ![Image Alt Text Convert Schema](https://mpbdevcontent.azureedge.net/Images/scenario-assets/convertschemacomplete.png)
