## Pre-migration overview

As you prepare for migrating to the cloud, verify that you are migrating from a MongoDB source with version 3.4  or earlier.

Please do not hesitate to reach out to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) with questions.

### Offline versus online migrations

When you migrate MongoDB data to Azure by using the Azure Database Migration Service, you can perform an offline or an online migration. With an *offline* migration, application downtime begins when the migration starts. For an *online* migration, downtime is limited to the time required to cut over to the new environment when the migration completes. It's recommended to test an offline migration to determine whether the downtime is acceptable; if not, perform an online migration.

### Additional resources

- For a matrix of the Microsoft and third-party services and tools that are available to assist you with various database and data migration scenarios as well as specialty tasks, see the article [Service and tools for data migration](https://docs.microsoft.com/azure/dms/dms-tools-matrix).
- For an overview of the Azure Database Migration Guide and the information it contains, see the video [How to Use the Database Migration Guide](https://azure.microsoft.com/resources/videos/how-to-use-the-azure-database-migration-guide/).
- For a walk through of the phases of the migration process and detail about the specific tools and services recommended to perform assessment and migration, see the video [Overview of the migration journey and the tools/services recommended for performing assessment and migration](https://azure.microsoft.com/resources/videos/overview-of-migration-and-recommended-tools-services/).
- For details about the pre-requirements, including Azure VNet and firewall set up, needed to create a DMS instance, see the video [How to address pre-requisites and create an instance of the Azure Database Migration Service](https://azure.microsoft.com/resources/videos/how-to-address-prerequisites-and-create-a-dms-instance/).
- For information about how to monitor an online migration and perform a migration cutover when the initial load and data sync have completed, see the video [How to monitor an online migration and perform migration cutover](https://azure.microsoft.com/resources/videos/how-to-monitor-online-migration-and-perform-cutover/).
- For a demo of how to migrate a MongoDB database to Cosmos DB, see the video [How to migrate MongoDB to Cosmos DB](https://azure.microsoft.com/resources/videos/how-to-migrate-mongodb-to-cosmos-db/).

### Preparation of target Cosmos DB account

1. You must create relevant Cosmos DB resources before migrating any data. Create an Azure Cosmos DB account and select MongoDB as the API. Pre-create your databases through the Azure portal. 

    ![Create a Cosmos DB account](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mongo-create-cosmos-account.png)

#### Request Units can be provisioned at two granularities 

- **Collection-level throughput:** Can be set for fixed collections or unlimited collections (with partitions). This is best for scenarios in which:
    - If there are a small number of Azure Cosmos DB containers.
    - If you want to get the guaranteed throughput on a given container backed by SLA.

- **Database-level throughput:** If throughput for the entire database will at least 400 RU/sec, it can be shared among any unlimited collections within the database, which can provide significant savings. Sharded MongoDB collections migrate to unlimited collections on Azure Cosmos DB and be eligible for database-level throughput. For MongoDB collections that are not sharded, it is easy to specify a partition key during the migration. This is best for scenarios in which you want to accommodate unplanned spikes in workloads by using pooled throughput at the database level.

2. For customers that are migrating many collections within a database, it is strongly recommend to configure database-level throughput. You must make this choice when you create the database. The minimum database-level [throughput capacity](https://docs.microsoft.com/azure/cosmos-db/request-units) is 400 RU/sec.
Each collection sharing database-level throughput requires at least 100 RU/sec. For example, if you are migrating 10 collections, database-level throughput must be at least 1,000 RU.

    ![Create a Cosmos DB database](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mongo-create-db.png)

3. Pre-create your collections through the Azure portal. It is strongly recommended that you create unlimited collections and specify a [shard key](https://docs.microsoft.com/en-us/azure/cosmos-db/partition-data). Setting the partition key/shard key, if applicable, must be done **prior** to the migration.

    ![Create a Cosmos DB collection](https://mpbdevcontent.azureedge.net/Images/scenario-assets/mongo-create-collection.png)

    Alternatively, you could create a fixed collection. You do not need to specify a partition key for fixed collection. Fixed collections have a 10GB max size.

    Collections can share the [throughput (RU/sec)](https://docs.microsoft.com/azure/cosmos-db/set-throughput) of a parent database if throughput has been defined at the database-level. You can also provision a dedicated amount of throughput (independent of the parent database) at the collection-level. If throughput is not defined at a database-level, it must be defined at the collection level.
    Both unlimited and fixed collections require a minimum of 400 RU/sec, when allocating dedicated throughput.

4. The duration of the migration will depend on the amount of throughput you set for each collection or database. For large data migrations, you should temporarily increase the throughput across your collections and databases.

### Overview of prerequisites

Before beginning your migration project, it is important to address the associated prerequisites. When moving data from MongoDB to Azure Cosmos DB, be sure to address the following prerequisites:

* Create an Azure Cosmos DB API for MongoDB account. (completed in the previous section).
* Create an Azure Virtual Network (VNET) for the Azure Database Migration Service by using the Azure Resource Manager deployment model.
* Ensure that VNET Network Security Group rules don't block the necessary communication ports.
* Open your Windows firewall to allow Azure DMS to access the source MongoDB server.

**Important**: For detail on the specific prerequisites associated with:
* Online migrations, see the information in [Migrate MongoDB to Azure Cosmos DB's API for MongoDB online using DMS](https://docs.microsoft.com/en-us/azure/dms/tutorial-mongodb-cosmos-db-online#prerequisites).
* Offline migrations, see the information in [Migrate MongoDB to Azure Cosmos DB's API for MongoDB offline using DMS](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db#prerequisites).
