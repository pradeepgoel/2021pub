![](./images/AZ-204-Labs-02-Flow.png)

## Lab 2 Build Azure functions using App Services
### Create resources
#### Storage account

    `az login`

* Create a resource group

    `az group create –resource-group  Serverless –location eastus`

* Create a storage account

    `az deployment group –resource-group Serverless –parameters storageAccountName=”functionstorepg” –template-uri <storage account uri>`

* Go to portal--> newly created storage account --> Copy connection string 

### Create a Function app
* Search for function app
* Create a function 
* In Basic -> resource group -> enter the name of app -> publish : code -> Runtime stack : .Net -> Version -> 3.1 Region -> east us
* Go to Hosting tab
* Storage account -> your storage account -> OS : linux -> Plan type : Consumption (serverless)
* review and create

## Create a local function project
* In visual studio code open folder

    cd F:\Allfiles\Labs\02\Starter\func
* Execute following command

    `func init –worker-runtime dotnet –force`

* Go to local.settings.json file

* Update AzureWebJobsStorage with earlier noted connection string

* Save the file
* Go to terminal

    `dotnet build`

* Local function project is created

### Create a function Echo

    func new –template “HTTP trigger” –name “Echo”
* In the Echo.cs file

* Update the code as per instructions and save

* Build the function

    `func start –build`

* Open a new Window Terminal and run following command

    `httprepl http://localhost:7071`

    * There will be an error navigate to following folder 

    `cd api`

    `cd echo`

* Test now posting an integer, string, and json method

`post –content 3`

`post –content “Hello”`

`post –content “{“msg”: “Successful”}”`

`exit`
