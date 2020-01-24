## Migrating from Cassandra

You can migrate Apache Cassandra data into Azure Cosmos DB via the Cassandra API.

A high-level outline of the process includes:

- Planning for moving the data
- Addressing the prerequisites for moving the data
- Moving the data by using:
  - The cqlsh COPY command
  - Spark

Using Cassandra API for Azure Cosmos DB has several benefits, including:

- **No operations management**: As a fully managed cloud service, Azure Cosmos DB Cassandra API removes the overhead of managing and monitoring a myriad of settings across OS, JVM, and yaml files and their interactions. 

- **Significant cost savings**: Customers on Cosmos DB Cassandra API can see major cost savings compared to customers using Cassandra on Iaas or On-Prem Cassandra. Customers using Cassandra on Iaas must pay for VM’s, bandwidth, and any applicable DSE licenses. Additionally, On-Prem Cassandra customers must manage their own data centers, servers, SSD storage, networking, and electricity costs. Cosmos DB customers have a simplified and smaller bill consisting of simply bandwidth, storage, and throughput.

- **Ability to use existing code and tools**: Azure Cosmos DB provides wire protocol level compatibility with existing Cassandra SDKs and tools. This compatibility ensures you can use your existing codebase with Azure Cosmos DB Cassandra API with trivial changes.

### Plan for moving data

Before moving Cassandra data to Azure Cosmos DB, estimate the throughput needs of your workload. In general, it's best to start with the average throughput required by the CRUD operations, and then include the additional throughput that is required for the Extract Transform Load (ETL) or spiky operations.

To plan for the move, you need to:

- **Determine the existing data size or estimated data size**: Define the minimum required database size and throughput. If you are estimating data size for a new application, assume that the data is uniformly distributed across the rows and estimate the value by multiplying with the data size.
- **Determine the required throughput**: Identify the approximate read (query/get) and write (update/delete/insert) throughput rate. This information is necessary to compute the required request units along with steady-state data size.
- **Export the schema**: Connect to your existing Cassandra cluster through cqlsh and export the schema from Cassandra:

    ```
        cqlsh [IP] "-e DESC SCHEMA" > orig_schema.cql
    ```

After you identify the requirements of your existing workload, create an Azure Cosmos DB account, database, and containers based on the gathered throughput requirements.

- **Determine the RU charge for an operation**: You can determine the RUs by using the Azure Cosmos DB Cassandra API SDK of your choice. This example shows the .NET version of getting RU charges.

    ```
        var tableInsertStatement = table.Insert(sampleEntity);
        var insertResult = await tableInsertStatement.ExecuteAsync();

        foreach (string key in insertResult.Info.IncomingPayload)

            {
            byte[] valueInBytes = customPayload[key];
            string value = Encoding.UTF8.GetString(valueInBytes);
            Console.WriteLine($"CustomPayload:  {key}: {value}");  
            }
    ```

- **Allocate the required throughput**: Azure Cosmos DB can automatically scale storage and throughput as your requirements grow. You can estimate your throughput needs by using the [Azure Cosmos DB request unit calculator](https://www.documentdb.com/capacityplanner).

### Prerequisites for moving data

- **Create tables in Azure Cosmos DB Cassandra API account**: Before you start the migrating data, pre-create all your tables from the Azure portal or from cqlsh. If you are migrating to an Azure Cosmos DB account that has database level throughput, make sure to provide a partition key when creating the Azure Cosmos DB containers.

- **Increase throughput**: The duration of your data migration depends on the amount of throughput you provisioned for the tables in Azure Cosmos DB. Increase the throughput for the duration of migration. With the higher throughput, you can avoid rate limiting and migrate in less time. After you've completed the migration, decrease the throughput to save costs. For more information about increasing throughput, see [set throughput](https://docs.microsoft.com/azure/cosmos-db/set-throughput) for Azure Cosmos DB containers. It’s also recommended to have Azure Cosmos DB account in the same region as your source database.

- **Enable SSL**: Azure Cosmos DB has strict security requirements and standards. Be sure to enable SSL when you interact with your account. When you use CQL with SSH, you have an option to provide SSL information.

### Options for moving data

You can move data from existing Cassandra workloads to Azure Cosmos DB by using either of the following options:

- The cqlsh COPY command
- Spark

### Move data using the cqlsh COPY command

You can use the [CQL COPY command](http://cassandra.apache.org/doc/latest/tools/cqlsh.html#cqlsh) to copy local data to Azure Cosmos DB via the Cassandra API. To copy the data, perform the following steps:

1. Make a note of the connection string information associated with your Cassandra API account:

    a. Sign in to the [Azure portal](https://portal.azure.com/), and then navigate to your Azure Cosmos DB account.

    b. Open the **Connection String** pane, which contains all the information that you need to connect to your Cassandra API account using cqlsh.

2. Sign in to cqlsh using the connection information you gathered from the portal.

3. Use the CQL COPY command to copy local data to the Cassandra API account.

    ```
        COPY exampleks.tablename FROM filefolderx/*.csv
    ```

### Move data using Spark

To move data to Azure Cosmos DB via the Cassandra API using Spark, perform the following steps:

1. Provision an [Azure Databricks](https://docs.microsoft.com/azure/cosmos-db/cassandra-spark-databricks) or a [HDInsight cluster](https://docs.microsoft.com/azure/cosmos-db/cassandra-spark-hdinsight).
2. Use the [table copy operation](https://docs.microsoft.com/azure/cosmos-db/cassandra-spark-table-copy-ops) to move data to the destination Cassandra API endpoint.

Moving data by using Spark jobs is the recommended option if you have data residing in an existing cluster in Azure virtual machines or in any other cloud. This requires that Spark be set up as intermediary for one-time or regular ingestion. You can accelerate this data movement by using express route connectivity between on-premises and Azure.

### Additional resources

To learn more about the Azure Cosmos DB Cassandra API, view the following resources:

- [Introduction to the Azure Cosmos DB Cassandra API](https://docs.microsoft.com/azure/cosmos-db/cassandra-introduction)
- [Apache Cassandra features supported by Azure Cosmos DB Cassandra API](https://docs.microsoft.com/azure/cosmos-db/cassandra-support)
- [Connect to Azure Cosmos DB Cassandra API from Spark](https://docs.microsoft.com/azure/cosmos-db/cassandra-spark-generic)

For a matrix of the Microsoft and third-party services and tools that are available to assist you with various database and data migration scenarios as well as specialty tasks, see the article [Service and tools for data migration](https://docs.microsoft.com/azure/dms/dms-tools-matrix).

**Videos**

- For an overview of the Azure Database Migration Guide and the information it contains, see the video [How to Use the Database Migration Guide](https://azure.microsoft.com/resources/videos/how-to-use-the-azure-database-migration-guide/).
- For a walk through of the phases of the migration process and detail about the specific tools and services recommended to perform assessment and migration, see the video [Overview of the migration journey and the tools/services recommended for performing assessment and migration](https://azure.microsoft.com/resources/videos/overview-of-migration-and-recommended-tools-services/).
