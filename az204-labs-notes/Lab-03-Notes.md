![](https://github.com/pradeepgoel/2021pub/blob/main/az204-labs-notes/images/AZ-204-Labs-05-Flow.png?raw=true)

## Lab 3 Build Azure functions using App Services
### Create resources
#### Storage account

* Login to Azure

    ```powershell
    az login
    ```


* Create a resource group

    ```powershell
    az group create –-resource-group  StorageMedia –-location eastus
    ```


* Create a storage account

    ```powershell
    az deployment group --resource-group StorageMedia --parameters storageAccountName=”functionstorepg” –-template-uri <storage account uri>
    ```

* Go to portal--> newly created storage account --> Copy Access key

### Create 2 containers and upload a file
* Go to portal --> Create containers --> "raster-graphic" and "compressed-audio"
* Set access of these containers as **Private (no anonymous access)**
* Go to "raster-graphic" container and upload file graph.jpg
* graph.jpg file is available in AllFiles/Labs/03/....

### Access containers using .NET program
* Go to VS code and open folder Allfiles (F):\Allfiles\Labs\03\Starter\BlobManager, and then select Select Folde
* Open Integrated Terminal
* Create following project
    ```powershell
    dotnet new console --name BlobManager --output .
    ```
* Import Azure.Storage.Blobs package
    ```powershell
    dotnet add package Azure.Storage.Blobs --version 12.0.0
    ```
* build project
    ```powershell
    dotnet build
    ```
### Modify Program.cs file as per instruction
* You will be doing following
    * Update blobServiceEndpoint, storageAccountName and storageAccountKey
    * Add all instructions and run the program
    * It will return Storage account properties
* Add methods for following
    * EnumarateContainersAsync, will return containers name
    * EnumarateBlobsAsync, will return blob uri from "raster-graphic" container
    * GetContainerAsync, will create a new container

* Run the program and test that all methods are working correctly

### Clear resources
* Execute following
    ```powershell
    az gruop delete --resource-group StorageMedia --no-wait --yes
    ```






