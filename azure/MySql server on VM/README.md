## Useful links
* [Hardening MySql Server][1] from digital ocean
* [vm-simple-linux][2] quick start template
* [GettingStarted-linux][3] Azure cli and ARM template

  [1]:https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04
  [2]:https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.compute/vm-simple-linux
  [3]:https://github.com/Azure/azure-quickstart-templates/blob/master/quickstarts/microsoft.compute/vm-simple-linux/GettingStarted-linux.md
  

## Setup a VM
* Loing to Azure
  * `az login`
* You will be navigated to browser, login into Azure and get back to terminal
* Create a new resource group
  ```
  az group create \
  --resource-group myResourceGroup \
  -- location eastus
  ```
* Create a VM using an ARM template, this template is avaialble at Azure quick start template
  ```
  az deployment group create \
  --name vmDeploymentWithARM \
  --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.compute/vm-simple-linux/azuredeploy.json
  ```
  * Provide user name and password on prompt
  * Upon successful creation of VM, go to Portal and go to resource group <resource group> name and note down the public ip address of the VM
  
 ## Access the VM and install MySql
 * From the terminal, enter following 
    `ssh <username>@<vm publiciP>`
 * Enter password on prompt
 * Upon login, execute following commands
  ```
  sudo apt update
  sudo apt install mysql-server
  ```
 * After installation is complete, execute `sudo mysql`
  
  ## Securing and accessing MySql Server remotely using MySQL Workbench
  * It is a good idea to secure your new installation and change default options for root and other sample users, run following command and follow instructions
   `sudo mysql_secure_installation`
  
 * Create a new user and grant privileges of root user
   
 `CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'password';`  
  
  * Grant all privileges on all databases
  `GRANT ALL PRIVILEGES ON *.* TO 'pkg'@'localhost' WITH GRANT OPTION;`
  
  * Flush privileges
  `FLUSH PRIVILEGES;`
  
  * Exit from mysql client
  `exit`
  
  * Next login into MySql server using the newly created user
  
## Accessing MySql database remotely using MySQL Serverbench__
  
  * Create a remoteuser
  ```
CREATE USER 'remoteuser'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'remoteuser'@'localhost WITH GRANT OPTION;
CREATE USER 'remoteuser'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'remoteuser'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
  
  ```
  
  * You will need to make update in the bind property
  * Go to 
  `/etc/mysql/mysql.conf.d`
  * Open file 
  `sudo vi mysqld.cnf`
  * Update bind-address to 0.0.0.0, it will allow connection from all machines, ideally you should update this address with your local address
  * Save changes and exit vi
  `:wq`
  * Need to restart MySQL server, run following 
  ```
  systemctl stop mysql.service
  systemctl start mysql.service
  
  ```
    
  * Check the status
  `systectl status mysql.service`
  
  * Go to MySql Serverbench
  * Select Standard TCP/IP over SSH
  * Use newly created user and you should be able to login
  * Run attached SQL script and a database will be created
  
  
## Clean up resources
  * Delete the resource group
   `az group delete --name myResourceGroup`
  
