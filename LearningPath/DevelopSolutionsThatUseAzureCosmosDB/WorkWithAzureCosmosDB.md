- Use `Microsoft.Azure.Cosmos` NuGet package
- `Container`: collection, graph or table
- `item`: document, edge/vertex, row. Content inside container

#### CosmosClient
`CosmosClient client = new CosmosClient(endpoint, key);`

#### Database example:
- **Create database**:
  - `CosmosClient.CreateDatabaseAsync` throws exception when database name already exists. <br>
  - `CosmosClient.CreateDatabaseIfNotExistsAsync`. Only database id is used to verify if exists
- **Read database by ID**:
  - `DatabaseResponse readResponse = await database.ReadAsync();`
- **Delete database**:
  - `await database.DeleteAsync();`

#### Container example
- **Create Container**
  - `await database.CreateContainerIfNotExistsAsync`
- **get container by ID**
  - `Container container = database.GetContainer(containerId)`
- **Delete container**
  - `await database.GetContainer(containerId).DeleteContainerAsync();`

#### Item example
- **Create item**
  - `ItemResponse<SalesOrder> response = await container.CreateItemAsync(salesOrder, new PartitionKey(salesOrder.AccountNumber));`
- **Read item**
  - `ItemResponse<SalesOrder> response = await container.ReadItemAsync(id, new PartitionKey(accountNumber));`
- **Query item**
  - `FeedIterator<SalesOrder> resultSet = container.GetItemQueryIterator<SalesOrder>`

# Create stored procedures
- Kinda like a function 
- Written in Javascript
- handling create/read/update/query/delete items inside cosmos container
- When you create item:
  - return the item id
  - it is async operation and uses Javascript callbacks.
  - Callback has 2 parameters:
    - Error object: handles error
    - Return value: contains created item
  - The procedure accepts a parameter (documentToCreate) that specifies the content of the document to be created.

# Create triggers and user-defined functions(UDF)
- `pretriggers`: executed before modifying a database item
- `posttriggers`: executed after modifying a database item.
- triggers are not automatically executed. It must be specified for each database operation.
- pretriggers cannot have any input parameters.

# Change feed
- The Change Feed in Azure Cosmos DB records container changes in order and outputs them for parallel, asynchronous processing.(basically: exposes events to outside world. you can use these)

- The Azure Cosmos DB change feed supports two models:
  - `Push Model`: The change feed processor handles state tracking and pushes changes to the client for processing.
    - 2 ways to read from a change feed:
      - Azure Functions Azure Cosmos DB triggers 
      - Change feed processor library
  - `Pull Model`: The client pulls changes, manages state, load balancing, and error handling.

- `Change feed processor`: simplifies the process of read change feed and distributing process
- 4 change feed processor components:
  - `Monitored Container`: Source of data; inserts and updates appear in the change feed.
  - `Lease Container`: Stores state and coordinates processing across workers.
  - `Compute Instance`: Hosts the processor, e.g., a VM, Kubernetes pod, or App Service.
  - `Delegate`: Defines the logic for handling each batch of changes.

The normal life cycle of a host instance is:
1. Read the change feed.
2. If there are no changes, sleep for a predefined amount of time (customizable with WithPollInterval in the Builder) and go to #1. 
3. If there are changes, send them to the delegate.
4. When the delegate finishes processing the changes successfully, update the lease store with the latest processed point in time and go to #1.
