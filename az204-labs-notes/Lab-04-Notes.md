![](./images/AZ-204-Labs-04-Flow.png)

## Lab 3 Build Azure functions using App Services
### Create resources
#### Storage account

* Login to Azure

    ```powershell
    az login
    ```


* Create a resource group

    ```powershell
    az group create –-resource-group  Polyglotdata –-location eastus
    ```


* Create a storage account

    ```powershell
    az deployment group --resource-group Polyglotdata --parameters storageAccountName=”polystorepg” –-template-uri <storage account uri>
    ```

* Go to portal--> newly created storage account --> Copy Access key


### Create container and upload a file

* Go to polystorepg1 account

* Create a container: images -> access level - public anonymous access -> upload all images from labs folder
* In the container blade -> properties -> copy URL value


### Create Cosmos DB resource
* In the Azure portal, execute following
    * Create a Cosmos DB account
    * Create: select core(SQL) recommended 
    * Select Polyglotdata resource group
    * Account name: polycosmos
    * Capacity mode: Serverless

* Once Cosmos account is created note down following:
    * URI
    * Primary Key
    * Primary Connection String

Review json data and upload to newly created cosmos data
 go to (F):\Allfiles\Labs\04\Starter\AdventureWorks\AdventureWorks.Upload, select models.json, and then select Open.
review the data especially Category, it will be used as partition key

### Clear resources
* Execute following
    ```powershell
    az gruop delete --resource-group StorageMedia --no-wait --yes
    ```






