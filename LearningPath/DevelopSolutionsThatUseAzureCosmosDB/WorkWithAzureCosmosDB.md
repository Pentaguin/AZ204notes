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
