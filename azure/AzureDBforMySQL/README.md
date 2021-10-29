## Useful Links
* Create [Azure DB for MySql][1] using Azure cli

* [Create a quick connect][2] using MySQL workbench

[1]:https://docs.microsoft.com/en-us/azure/mysql/quickstart-create-mysql-server-database-using-azure-cli

[2]:https://docs.microsoft.com/en-us/azure/mysql/connect-workbench

## Setup

* Login to Azure from mac terminal
  * `az login`

* Upon redirection to Azure login browser window, enter your credentials
* Return to the terminal
* Create a resource group
  * `az group create --name myresourcegroup --location westus`
* Create an Azure database for MySQL Server using the resource group created in the previous step
  * `az mysql server create --resource-group myresourcegroup --name mydemoserver --location westus --admin-user myadmin --admin-password <server_admin_password> --sku-name GP_Gen5_2 </code>`
* Database is created, review and note down from the output
  * Connection string
  * Fully qualified domain name

* Create firewall rule and allow connection from your local machine
  * `az mysql server firewall-rule create --resource-group myresourcegroup --server mydemoserver --name AllowMyIP --start-ip-address 192.168.0.1 --end-ip-address 192.168.0.1`
* How to find out local machine IP, execute following from your terminal
  * `curl ifconfig.me/ip`
  * Use retrieved ip address for start and end ip address
 
## Connect using Bash or MySql Workbench
  * for bash
   * `mysqlsh -h azdbformysqldemodb.mysql.database.azure.com -u myadmin@azdbformysqldemodb -p`
  * For MySql Workbench
    * create a connection by providing DB details
    * test connection
    * execute mytestdb.sql file, this file will create a DB, table, insert and update data
  
  ## Clean up resources
  * Delete resource group
    * `az group delete --name myresourcegroup`
  * Delete database
    * `az mysql server delete --resource-group myresourcegroup --name mydemoserver`
      
