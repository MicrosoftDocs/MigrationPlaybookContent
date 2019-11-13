## Pre-migration overview

After verifying that your source environment is supported and ensuring that you have addressed any prerequisites, you are ready to start the Pre-migration stage. This part of the process involves conducting an inventory of the databases that you need to migrate, assessing those databases for potential migration issues or blockers, and then resolving any items you might have uncovered. For heterogenous migrations such as Oracle to Azure Database for PostgreSQL, this stage also involves converting the schema(s) in the source database(s) to be compatible with the target environment.

## Discover


The goal of the Discover phase is to identify existing data sources and details about the features that are being used to get a better understanding of and plan for the migration. This process involves scanning the network to identify all your organization’s Oracle instances together with the version and features in use.

### Steps

To use the MAP Toolkit to perform an inventory scan, perform the following steps.

1. **Download the [MAP Toolkit](http://go.microsoft.com/fwlink/?LinkID=316883)**, and then install it.

2. **Run the MAP toolkit**.

    a. Open the MAP toolkit, and then on the left pane, select **Database**.
    
    You will be on the following screen:
    
    ![MAP Overview](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapoverview.png)
    
    b. Select **Create/Select database**.
    
    ![MAP Create/Select DB](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapselectdb.png)
     
    c. Ensure that **Create an inventory database** is selected, enter a name for the database, a brief description, and then select **OK**.
    
    ![MAP Create/Select DB Overview](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapselectdboverview.png)
    
    The next step is to collect data from the database created.
    
    d. Select **Collect inventory data**.
    
    ![MAP Collect Inventory Data](https://mpbdevcontent.azureedge.net/Images/scenario-assets/maporacleoverview.png)
    
    e. In the Inventory and Assessment Wizard, select **Oracle**, and then select **Next**.
    
    ![MAP Inventory and Assessment Wizard](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapinventorywizard_oracle.png)
    
    f. Select the best method option to search the computers on which Microsoft Products are hosted, and then select **Next**.
    
    ![MAP Inventory and Assessment Wizard Discovery Methods](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapdiscoverymethods.png)
    
    g. Enter credentianls or create new credentials for the systems that you want to explore, and then select **Next**.
    
    ![MAP Inventory and Assessment Wizard Discovery Credentials](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapdiscoverycreds.png)
    
    h. Set the order of the credentials.
    
    ![MAP Inventory and Assessment Wizard Discovery Credentials Order](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapdiscoverycredsorder2.png)
    
    Now, you need to specify the credentials for each computer you want to discover. You can use unique credentials for every computer/machine, or you can choose to use the **All Computer Credentials** list.
    
    i. After setting up the credentials, select **Save**, and then select **Next**.
    
    ![MAP Inventory and Assessment Wizard Discovery Credentials](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapdiscoverycredsindividual.png)
    
    j. Verify your selection summary, and then select **Finish**.
    
    ![MAP Inventory and Assessment Wizard Summary](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapdiscoverysummary.png)
    
    k. Wait for a few minutes (depending on the number of databases) for the Data Collection summary report.
    
    ![MAP Inventory and Assessment Wizard Summary](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapdatacollectionsummary.png)
    
    l. Select **Close**.
    
    The Main window of the tool appears, showing a summary of the Database Discovery completed so far.
    
 3. **Report generation and data collection**.
    
    On top right corner of the tool, an **Options** page appears, which you can use to generate a report about the Oracle Assessment and the Database Details.
       
    a. Select both options (one by one) to generate the report.
    
    This will take a couple of seconds to a few minutes depending upon the size of the inventory comlpeted during discovery.
    
    ![MAP Report Generation](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mapexcelreportdone.png)

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

   ![Image Alt Text New Project](https://mpbdevcontent.azureedge.net/Images/scenario-assets/newproject.png)

   c. Select **Connect to Oracle**, provide the connection details, and then select **Connect**.
   
   ![Image Alt Text Connect to Oracle](https://mpbdevcontent.azureedge.net/Images/scenario-assets/connecttooracle.png)
   
   d. In the **Oracle Metadata Explorer**, select the Oracle schema, and then select **Create Report** to create the conversion report.
   
   ![Image Alt Text Create Report](https://mpbdevcontent.azureedge.net/Images/scenario-assets/createreport.png)
   
    This will generate an HTML report with conversion statistics and error/warnings, if any.
     
   e. Analyze this report to understand any conversion issues and their cause.
   
   ![Image Alt Text Assessment Report](https://mpbdevcontent.azureedge.net/Images/scenario-assets/assessmentreport.png)
   
   You can also access this report from the SSMA projects folder as selected in the first screen.
   
   f. From the example above locate the report.xml file from: 
   
   *drive:*\Users\<username>\Documents\SSMAProjects\MyOracleMigration\report\report_2016_11_12T02_47_55\
   
   and then open it in Excel to get an inventory of Oracle objects and the effort required to perform schema conversions.
   
3. **Perform schema conversion**.

   a. Before you perform schema conversion, validate the default datatype mappings or change them based on requirements.
   
   You could do this either by navigating to the **Tools** menu and selecting **Project Settings** or by changing the type mapping for each table by selecting the table in the **Oracle Metadata Explorer**.
   
   ![Image Alt Text Type Mappings](https://mpbdevcontent.azureedge.net/Images/scenario-assets/typemappings.png)
   
   You can add dynamic or ad hoc queries to the **Statements** node by selecting that node and then selecting **Add Statement** on the right-click menu.
   
   b. To convert and move the schema to SQL Server, connect to the SQL server instance by providing the connection details in the **Connect to SQL Server** dialog box.
   
   You can choose to connect to an existing database or provide a new name, in which case a database will be created on the target server.
   
   ![Image Alt Text Connect to SQL](https://mpbdevcontent.azureedge.net/Images/scenario-assets/connecttosql.png)
   
   c.	Convert the schema by selecting **Convert Schema** from the right-click menu or the menu bar on the top.
   
   ![Image Alt Text Convert Schema](https://mpbdevcontent.azureedge.net/Images/scenario-assets/convertschema.png)
   
   d.	After schema conversion, compare and review the structure of the schema to identify potential problems.
   
   ![Image Alt Text Convert Schema](https://mpbdevcontent.azureedge.net/Images/scenario-assets/convertschemacomplete.png)
