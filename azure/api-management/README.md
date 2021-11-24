## Useful link
* [quick-start-link][1]
* [api-gateway-management][2] overview 

[1]:https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.apimanagement
[2]:https://docs.microsoft.com/en-us/azure/api-management/api-management-key-concepts

## Setup
* Login to portal `az login`
* Create a resource group
    * `az group create --resource-group apimRG --location eastUS`
* Deploy an apim instance
    * `az apim create --name myapimGW --resource-group apimRG 
  --publisher-name testApim 
  --publisher-email pradeepgoel01@gmail.com 
  --no-wait`
* Check the apim status
    * `az apim show --name myapimGW --resource-group apimRG --output table`

## Cleanup resources
* Go to portal and delete the instance
