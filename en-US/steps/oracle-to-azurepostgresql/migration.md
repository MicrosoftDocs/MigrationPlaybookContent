## Migration overview

After you have the necessary prerequisites in place and have completed the tasks associated with the **Pre-migration** stage, you are ready to perform the schema and data migration.

## Migrate schema and data

After the fixes are in place, a stable build of the database is ready for deployment. 

At this point, all that is required is to execute the *psql* import commands, pointing to the files containing the modified code in order to compile the database objects against the PostgreSQL database and import the data. 

In this step, some level of parallelism on importing the data can be implemented.

## Data sync and Cutover

With online (minimal-downtime) migrations, the source you are migrating continues to change, drifting from the target in terms of data and schema, after the one-time migration occurs. During the **Data sync** phase, you need to ensure that all changes in the source are captured and applied to the target in near real time. After you verify that all changes in source have been applied to the target, you can cutover from the source to the target environment.

As of March 2019, if you want to perform an online migration, consider using Attunity Replicate for Microsoft Migrations or Striim.

For “delta/incremental” migration using ora2pg, the technique consists in applying for each table a query that applies a filter (cut) by date or time, etc., and after that finalizing the migration applying a second query which will migrate the rest of the data (leftover).

In the source data table, migrate all the historical data first. An example of that is: 

```
select * from table1 where filter_data < 01/01/2019 
```

You can query the changes made since the initial migration by running a command similar to the following: 

```
select * from table1 where filter_data >= 01/01/2019 
```

In this case it is recommended that the validation is enhanced by checking data parity on both sides, source and target.
