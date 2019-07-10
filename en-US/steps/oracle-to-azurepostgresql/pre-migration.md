## Pre-migration overview

After verifying that your source environment is supported and ensuring that you have addressed any prerequisites, you are ready to start the Pre-migration stage. This part of the process involves conducting an inventory of the databases that you need to migrate, assessing those databases for potential migration issues or blockers, and then resolving any items you might have uncovered. For heterogenous migrations such as Oracle to Azure Database for PostgreSQL, this stage also involves converting the schema(s) in the source database(s) to be compatible with the target environment.

## Discover

The goal of the Discover phase is to identify existing data sources and details about the features that are being used to get a better understanding of and plan for the migration. This process involves scanning the network to identify all your organization’s Oracle instances together with the version and features in use.

Microsoft Oracle pre-assessment scripts run against the Oracle database. The Pre-assessment script are a set of queries that hits the Oracle metadata and provides the following: 

- Database inventory, including counts of objects by schema, type, and status.
- A rough estimate of Raw Data in each schema (based on statistics).
- Sizing of tables in each schema.
- The number of lines of code per Package, Function, Procedure, etc.

Download the related scripts from the [ora2pg website](http://ora2pg.darold.net/).

## Assess

After completing the inventory of the Oracle database(s) to get an idea of the database size and what the challenges are, the next step is to run the Assessment.

Estimating the cost of a migration process from Oracle to PostgreSQL is not easy. To obtain a good assessment of this migration cost, ora2pg will inspect all database objects, all functions and stored procedures to detect if there are still some objects and PL/SQL code that cannot be automatically converted by ora2pg.

ora2pg has a content analysis mode that inspect the Oracle database to generate a text report on what the Oracle database contains and what cannot be exported. 

To activate the "analysis and report" mode, use the export de type SHOW_REPORT as shown in the following command:

```
ora2pg -t SHOW_REPORT 
```

After the database is analyzed, ora2pg, with its ability to convert SQL and PL/SQL code from Oracle syntax to PostgreSQL, can go further by estimating the code difficulties and the time necessary to perform a full database migration.

To estimate the migration cost in man-days, ora2pg allows you to use a configuration directive called ESTIMATE_COST, which can also be enabled at command line: 

```
ora2pg -t SHOW_REPORT --estimate_cost 
```

The default migration unit represent around five minutes for a PostgreSQL expert. If this is your first migration you can get it higher with the configuration directive COST_UNIT_VALUE or the --cost_unit_value command line option.

The last line of the report shows the total estimated migration code in man-days following the number of migration units estimated for each object. This migration unit represents around five minutes for a PostgreSQL expert. If this is your first migration, you can increase the default with the configuration directive COST_UNIT_VALUE or the --cost_unit_value command line option. Find below some variations of assessment a) tables assessment; b) columns assessment c) schema assessment using default cost_unit (5 min) d) schema assessment using 10 min as cost unit.

```
ora2pg -t SHOW_TABLE -c c:\ora2pg\ora2pg_hr.conf > c:\ts303\hr_migration\reports\tables.txt ora2pg -t SHOW_COLUMN -c c:\ora2pg\ora2pg_hr.conf > c:\ts303\hr_migration\reports\columns.txt 
ora2pg -t SHOW_REPORT -c c:\ora2pg\ora2pg_hr.conf --dump_as_html --estimate_cost > c:\ts303\hr
_migration\reports\report.html  
ora2pg -t SHOW_REPORT -c c:\ora2pg\ora2pg_hr.conf –-cost_unit_value 10 --dump_as_html --estima te_cost > c:\ts303\hr_migration\reports\report2.html  
```

The output of the schema assessment is illustrated as below:

**Migration level: B-5**

```
    Migration levels: 
    A - Migration that might be run automatically 
    B - Migration with code rewrite and a human-days cost up to 5 days
    C - Migration with code rewrite and a human-days cost above 5 days 
    Technical levels: 
    1 = trivial: no stored functions and no triggers 
    2 = easy: no stored functions but with triggers, no manual rewriting 
    3 = simple: stored functions and/or triggers, no manual rewriting 
    4 = manual: no stored functions but with triggers or views with code rewriting 
    5 = difficult: stored functions and/or triggers with code rewriting
```

The assessment consists in a letter (A or B) to specify whether the migration needs manual rewriting or not, and a number from 1 to 5 to indicate the technical difficulty level. You have an additional option -human_days_limit to specify the number of human-days limit where the migration level should be set to C to indicate that it needs a huge amount of work and a full project management with migration support. Default is 10 human-days. You can use the configuration directive HUMAN_DAYS_LIMIT to change this default value permanently. 

This feature has been developed to help deciding which database could be migrated first and what is the team that need be mobilized.

## Convert

With minimal-downtime migrations, the source you are migrating continues to change, drifting from the target in terms of data and schema, after the one-time migration occurs. During the **Data sync** phase, you need to ensure that all changes in the source are captured and applied to the target in near real time. After you verify that all changes in source have been applied to the target, you can cutover from the source to the target environment.

In this step of the migration, the conversion or translation of the Oracle Code + DDLS to PostgreSQL occurs. The ora2pg tool exports the Oracle objects in a PostgreSQL format automatically. For those objects generated, some won’t compile in the PostgreSQL database without manual changes.  
The process of understanding which elements need manual intervention consists in compiling the files generated by ora2pg against the PostgreSQL database, checking the log and making the necessary changes until all the schema structure is compatible with PostgreSQL syntax. 

1. First, it is recommended to create the migration template that is provided out of the box with ora2pg. The two options --project_base and --init_project when used indicate to ora2pg that it has to create a project template with a work tree, a configuration file and a script to export all objects from the Oracle database. For further information, consult the ora2pg [documentation](https://ora2pg.darold.net/documentation.html).

        The command is executed show in the following example:

```
        ora2pg --project_base /app/migration/ --init_project test_project
```

```
        ora2pg --project_base /app/migration/ --init_project test_project
                Creating project test_project.         /app/migration/test_project/                 schema/                         dblinks/                         directories/                         functions/                         grants/                         mviews/                         packages/                         partitions/                         procedures/                         sequences/                         synonyms/                         tables/                         tablespaces/                         triggers/                         types/                        views/                 sources/                         functions/                         mviews/                         packages/                         partitions/                         procedures/                         triggers/                         types/                         views/                 data/                 config/                 reports/ 

                Generating generic configuration file 
                Creating script export_schema.sh to automate all exports. 
                Creating script import_all.sh to automate all imports.
```

        The sources/ directory contains the Oracle code, the schema/ directory contains the code ported to PostgreSQL. The reports/ directory contains the html reports with the migration cost assessment. 

        After the project structure is created, a generic config file is created. Define the Oracle database connection as well as the relevant config parameters in the config. Refer to the ora2pg documentation to understand what can be configured in the config file and how.

2. Next, export the Oracle objects as PostgreSQL objects by running the file export_schema.sh.

```
        cd /app/migration/mig_project
        ./export_schema.sh 
```

        Run the following command manually:

```
        SET namespace="/app/migration/mig_project" 
        
                ora2pg 	-t 	DBLINK 	-p 	-o 	dblink.sql 	-b 	%namespace%/schema/dblinks 	-c 
        %namespace%/config/ora2pg.conf 
        ora2pg -t DIRECTORY -p -o directory.sql -b %namespace%/schema/directories -c 
        %namespace%/config/ora2pg.conf 
        ora2pg -p -t FUNCTION -o functions2.sql -b %namespace%/schema/functions -c 
        %namespace%/config/ora2pg.conf ora2pg -t GRANT -o grants.sql -b %namespace%/schema/grants -c %namespace%/config/ora2pg.conf ora2pg -t MVIEW -o mview.sql -b %namespace%/schema/mviews -c %namespace%/config/ora2pg.conf 
        ora2pg -p -t PACKAGE -o packages.sql 
        %namespace%/config/ora2pg.conf 	-b %namespace%/schema/packages 	-c 
        ora2pg -p -t PARTITION -o partitions.sql %namespace%/config/ora2pg.conf 	-b %namespace%/schema/partitions 	-c 
        ora2pg -p -t PROCEDURE -o procs.sql 
        %namespace%/config/ora2pg.conf 	-b %namespace%/schema/procedures 	-c 
        ora2pg -t SEQUENCE -o sequences.sql 
        %namespace%/config/ora2pg.conf 	-b %namespace%/schema/sequences 	-c 
        ora2pg -p -t SYNONYM -o synonym.sql 	-b %namespace%/schema/synonyms 	-c 
        %namespace%/config/ora2pg.conf 
        ora2pg -t TABLE -o table.sql -b %namespace%/schema/tables -c %namespace%/config/ora2pg.conf ora2pg -t TABLESPACE -o tablespaces.sql -b %namespace%/schema/tablespaces -c 
        %namespace%/config/ora2pg.conf 
        ora2pg -p -t TRIGGER -o triggers.sql -b %namespace%/schema/triggers -c 
        %namespace%/config/ora2pg.conf ora2pg -p -t TYPE -o types.sql -b %namespace%/schema/types -c %namespace%/config/ora2pg.conf ora2pg -p -t VIEW -o views.sql -b %namespace%/schema/views -c %namespace%/config/ora2pg.conf  
```

        To extract the data, use the following command: 

```
        ora2pg -t COPY -o data.sql -b %namespace/data -c %namespace/config/ora2pg.conf 
```

3. Lastly, compile all files against Azure Database for PostgreSQL server. It is possible now to choose to load the DDL files generated manually or use the second script import_all.sh to import those files interactively.  

```
        psql 	-f 	%namespace%\schema\sequences\sequence.sql 	-h 	server1-
        server.postgres.database.azure.com -p 5432 -U username@server1-server -d database -l 
        %namespace%\ schema\sequences\create_sequences.log 
        psql -f %namespace%\schema\tables\table.sql -h server1-server.postgres.database.azure.com p 5432 -U username@server1-server -d database -l %namespace%\schema\tables\create_table.log 
```

        Data import command: 

```
        psql -f %namespace%\data\table1.sql -h server1-server.postgres.database.azure.com -p 5432 -U username@server1-server -d database -l %namespace%\data\table1.log 
        psql -f %namespace%\data\table2.sql -h server1-server.postgres.database.azure.com -p 5432 -U username@server1-server -d database -l %namespace%\data\table2.log 
```

        During the compilation of files, check the logs and correct the necessary syntaxes that ora2pg was unable to convert out of the box. 

Refer to the white paper [Oracle to Azure Database for PostgreSQL Migration Workarounds](https://github.com/Microsoft/DataMigrationTeam/blob/master/Whitepapers/Oracle%20to%20Azure%20Database%20for%20PostgreSQL%20Migration%20Workarounds.pdf) for support on working around issues.
