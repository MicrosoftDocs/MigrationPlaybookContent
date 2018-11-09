<!--Pre-migration overview-->

As you prepare for migrating to the cloud, verify that you are migrating from a MongoDB source with version 3.4  or earlier.

Please do not hesitate to reach out to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) with questions.

### Preparation of target Cosmos DB account

1. You must create relevant Cosmos DB resources before migrating any data. Create an Azure Cosmos DB account and select MongoDB as the API. Pre-create your databases through the Azure portal. 

    ![Create a Cosmos DB account](https://mpbdevcontent.azureedge.net/Images/mongo-create-cosmos-account.png)


#### Request Units can be provisioned at two granularities 
 

**Collection-level throughput:** 

- Can be set for fixed collections or unlimited collections (with partitions) 
 

    *When is this best?* 

    - If there are a small number of Azure Cosmos DB containers 
    - If you want to get the guaranteed throughput on a given container backed by SLA 

**Database-level throughput:** 

- If throughput for the entire database will be over 10,000 RU’s, it can be shared among any unlimited collections within the database. This can provide significant savings.
- If MongoDB collections were sharded, they can migrate to unlimited collections on Cosmos DB and be eligible for database-level throughput. If MongoDB collections are not sharded, it is easy to specify a partition key during the migration 

    *When is this best?* 

    - If you want to consider unplanned spikes in workloads by using pooled throughput at the database level 

2. For customers that are migrating many collections within a database, it is strongly recommend to configure database-level throughput. You must make this choice when you create the database. The minimum database-level [throughput capacity](https://docs.microsoft.com/azure/cosmos-db/request-units) is 10,000 RU’s.

    ![Create a Cosmos DB database](https://mpbdevcontent.azureedge.net/Images/mongo-create-db.png)

3. Pre-create your collections through the Azure portal. It is strongly recommended that you create unlimited collections and specify a [shard key.](https://docs.microsoft.com/en-us/azure/cosmos-db/partition-data) These have a minimum throughput capacity of 1,000 RU’s. Creating a partition key/shard key, if applicable, should be done **prior** to the migration.

    ![Create a Cosmos DB collection](https://mpbdevcontent.azureedge.net/Images/mongo-create-collection.png)

    Alternatively, you could create a fixed collection. You do not need to specify a partition key for fixed collection and the minimum throughput capacity is 400 RU’s. Fixed collections have a 10GB max size.

4. If you did not choose to provision database-level throughput, you should specify the throughput for each collection. 

    ![Create a Cosmos DB collection - details](https://mpbdevcontent.azureedge.net/Images/mongo-create-collection2.png)

5. The duration of the migration will depend on the amount of throughput you set for each collection or database. For large data migrations, you should temporarily increase the throughput across your collections and databases.
