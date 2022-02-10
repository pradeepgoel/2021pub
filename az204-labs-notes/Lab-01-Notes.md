
## Lab 1 Build a Web Application to upload and display images from Azure Storage
### Create resources

`az login`

* Create a resource group named ManagedPlatform

`az group create –resource-group ManagedPlatform –location eastus`

* Upon successful creation run following command to create a storage account

`az deployment group create –resource-group ManagedPlatform –name imagestor –template-uri <template-uri-path>`

* Go to portal and navigate to newly created storage account
* Go to networking + security -> access keys
* Show access keys
* Copy any connection string to notepad

* Create a blob container
    * Go to storage account, select container from the left nav menu
    
    * Enter name:images

    * Select blob (anonymous access for read blob only)
    * Upload grilledchees.jpg from F: folder

### Deploy a web app
`az deploy group create –resource-group ManagedPlatform –parameters language=”.net” sku=”S1” repoUrl=”<enter repo url>”   webAppName=”<your web app name>” –template-uri=https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.web/webapp-basic-windows/azuredeploy.json`


* Once deployment is complete, go to app services in the portal, go to newly created app
* Go to configuration -> application settings -> enter StorageConnectionString and enter earlier copied connection string value, save and continue

* On the properties -> copy app url value

### Deploy a .Net program 

* In Visual Studio code -> open folder
F: \Allfiles\labs\01\starter\API

* Open ImageController.cs program and review
Right click and Open Integrated Terminal

`az login`

`az webapp list --resource-group ManagedPlatform --query "[?starts_with(name, 'imgapi')].{Name:name}" --output tsv`

* Your newly created app will be listed
* Go to cd F:\Allfiles\Labs\01\Starter\API\

* Enter following command to deploy the app

`az webapp deployment source config-zip --resource-group ManagedPlatform --src api.zip --name <name-of-your-api-app>`

* Go To Portal and navigate to imgapipg app and from app services click on browse, a json object will be returned

### Deploy a frontend app

* Execute following from the terminal

`az deploy group create --resource-group ManagedPlatform -–parameters language=”.net” sku=”S1” repoUrl=”<enter repo url>”   webAppName=”<imgwebpg1>” --template-uri=https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.web/webapp-basic-windows/azuredeploy.json`


* Once webapp is created, execute following to list newly created app

`az webapp list --resource-group ManagedPlatform --query "[?starts_with(name, 'imgweb')].{Name:name}" --output tsv`

* Go to portal, select newly created webapp, go to settings -> configuration , create new application settings, enter name “ApiUrl” - in the value enter url of imgapipg1 Url

* Go to Visual Studio Code

* Open 
cd F:\Allfiles\Labs\01\Starter\Web\
* review index.cshtml.cs file

* Deploy webapp 

`az webapp deployment source config-zip --resource-group ManagedPlatform --src web.zip --name <name-of-your-web-app>`

* Now go back to portal, go to this application and “Browse”
in the browser window, your app will be opened

* Note, grilledcheese image will be there
click on upload image and upload an image
that image will also appear on the page
