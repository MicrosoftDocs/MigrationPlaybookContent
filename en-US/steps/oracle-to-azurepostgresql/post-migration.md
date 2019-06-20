## Post-migration overview

After you have successfully completed the **Migration** stage, you need to go through a series of post-migration tasks to ensure that everything is functioning as smoothly and efficiently as possible.

## Remediate applications

After the data is migrated to the target environment, all the applications that formerly consumed the source need to start consuming the target. Accomplishing this will in some cases require changes to the applications.

## Perform tests

After the data is migrated to target, perform tests against the databases to verify that the applications perform well against the after the migration.

To guarantee that the source and target are properly migrated, run the manual data validation scripts against the Oracle source and PostgreSQL target databases.

Ideally, if the source and target databases have a networking path, ora2pg should be used for data validation. Using the TEST action allows you to check that all objects from the Oracle database have been created under PostgreSQL. Run the command as shown:

```
ora2pg -t TEST -c config/ora2pg.conf > migration_diff.txt 
```

## Optimize

The post-migration phase is crucial for reconciling any data accuracy issues and verifying completeness, as well as addressing performance issues with the workload.