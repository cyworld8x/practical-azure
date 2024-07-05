**The Azure CLI command essentials **
-----------------------------------

To log in to your Azure subscription is:


`   az login   `

**Optional flags:**

While az login works for basic login, there are some optional arguments that can be useful:

*   \--use-device-code: Forces the use of the device code authentication method.
    
*   \--tenant : Specifies the Azure Active Directory tenant to sign in to (relevant for multi-tenant environments).
    
*   \--service-principal: Use this flag if you want to authenticate using a service principal (application identity) instead of your user account.
    

**Example:**

`   az login --use-device-code `

To create a resource group is:

`az group create --name <resouce-grpup-name> --location <location>` 

**Example**

`az group create --name myResourceGroup --location eastasia` 

**Breakdown of the command:**

*   az group create: This part of the command specifies that you want to use the Azure CLI group extension to create a resource group.
    
*   \--name : This option is mandatory and requires you to replace with a unique name for your resource group. Choose a name that reflects the resources you plan to place within the group.
    
*   \--location : This option is also mandatory and specifies the Azure region where you want to create the resource group. You can find a list of supported regions using az location list.
    

To remove a resource group:

`   az group delete --name`

**Example**

`   az group delete --name myResourceGroup`

**Breakdown of the command:**

*   az group delete: This part of the command specifies that you want to use the Azure CLI group extension to delete a resource group.
    
*   \--name : This option is mandatory and requires you to replace with the actual name of the resource group you want to delete.
    

**Additional Options:**

*   \--force-deletion -f: This flag forces the deletion of the resource group even if there are running resources within it. Use this option cautiously as it can lead to data loss.
    
*   \--ids : This option allows you to specify the resource group using its ID instead of the name. You can find the resource group ID using the az group list command.

To list out resource groups:

`   az group list`


Azure CLI commands to create and remove an Azure Container Registry (ACR):

**Create an ACR:**

`   az acr create --name <acr-name> --resource-group <resource-group-name> location <location> [--sku <sku>]`

*   \<acr-name\>: Replace this with a unique name for your ACR (must be lowercase alphanumeric characters with a length of 5-50).
    
*   \<resource-group-name\>: The name of the resource group where you want to create the ACR. You can create a new resource group using az group create or use an existing one.
    
*   \<location\>: Specify the Azure region where you want to create the ACR. Use az location list to see available regions.
    
*   \[ --sku \] (optional): This option allows you to specify the SKU (pricing tier) for your ACR. Choose from Basic, Standard, or Premium based on your needs. Defaults to Basic if not specified.
    

**Example:**

`   az acr create --name myacr --resource-group myResourceGroup --location eastasia --sku Standard --admin-enabled true `

This command creates an ACR named "myacr" in the "myResourceGroup" resource group located in the East Asia (eastasia) region with the Standard pricing tier.

**Remove an ACR:**

`az acr delete --name <acr-name>` 

*   \<acr-name\>: Replace this with the name of the ACR you want to delete.
    

**Important Note:**

*   Deleting an ACR is permanent and removes all images stored within it. Ensure you've backed up any necessary images before deletion.
    
*   By default, Azure CLI will prompt you for confirmation before deleting the ACR. You can bypass this confirmation by adding the --yes -y flag at the end of the command. However, use this option with caution as it skips confirmation.
    

**Additional Options for az acr create:**

*   \--admin-enabled {false, true}: Enables or disables admin user creation for the ACR (defaults to false).
    
*   \--allow-exports {false, true}: Controls whether images can be exported from the ACR (defaults to false).
    

Commands to manage (Create/Delete) the image on acr
---------------------------------

Here are the necessary Azure CLI commands to push an image to your Azure Container Registry (ACR):

**1\. Login to ACR:**

`az acr login --name <acr-name>` 

*   Replace with the actual name of your Azure Container Registry.
*   **Note**: Needs a running docker to execute command.

**1.1\. Set default resource group to work on (#Default#)** 

`az configure --defaults group=<name>`

**2\. Build and tag the image (assuming you have a Dockerfile in your current directory):**

`   docker build -t <acr-name>.azurecr.io/<image-name>:<tag>  `

*   \<acr-name\>.azurecr.io: This is the login server name for your ACR.
    
*   \<image-name\>: The name you give to your image within the ACR.
    
*   \<tag\>: A version tag for your image (e.g., v1.0, latest).
    

**3\. Push the image to ACR:**

`   az acr push --name <acr-name> --image <image-name>:<tag>   `

*   \<acr-name\>: Same as in step 1.

*   \<image-name\>: Same as in step 2.

*   \<tag\>: Same as in step 2.

**3.1\. Or Docker to Push the image to ACR:**

`  docker push <image-name>:<tag>   `

*But before that should command docker login

`   docker login <acr-name>.azurecr.io`

*   \<acr-name\>: Same as in step 1.

*   \<image-name\>: Same as in step 2.

*   \<tag\>: Same as in step 2.

**Explanation:**

*   The first command logs you in to your ACR using the az acr login command.
    
*   The second command builds a Docker image using the docker build command. It tags the image with the following format:
    
    *   \<acr-name\>.azurecr.io: This identifies your ACR.
        
    *   \<image-name\>: The name you assign to the image within your ACR.
        
    *   \<tag\>: A version tag for your image, allowing you to keep track of different versions.
        
*   The third command uses az acr push to push the built and tagged image to your ACR.


**To very image**

`    az acr repository show --name <acr-name> --repository <image-name> --resource-group <resouce-group>  `

*   \<acr-name\>: Same as in step 1.

*   \<image-name\>: Same as in step 2.

*   \<tag\>: Same as in step 2.

*   \<resouce-group\>: Specify resource group name, or can be removed by doing step 1.1 to set default group name.

**Example**
`   az configure defaults group=<resource-group-name>`
`    az acr repository show --name <acr-name> --repository <image-name> --resource-group <resouce-group>  `

**To list repositories**

` az acr repository list --name <acr-name>`

**To delete image**

` az acr repository delete --name <acr-name> --image <image-name>:<tag>`

**To delete untagged images**

` az acr repository delete --name <acr-name> --force`

*   Using --force with az acr repository delete is permanent and cannot be undone.

**Creating, Running and Stopping Containers on Azure Container Instances (ACI)**

**Run a container from an ACR image:**

`az container create --name <container-name> --image <acr-name>.azurecr.io/<image-name>:<tag> --dns-name-label <dns-name> --registry-username <username> --registry-password <password>`

* This command needs credentail to login the acr by admin account. By enableing admin, You can enable the admin user in the Azure portal by navigating your registry, selecting "Access keys" under SETTINGS, then Enable under Admin user to get two password.*

`   az acr update -n <acrName> --admin-enabled true`

There are few other ways to do that:  

*   Use individual Azure identity*

` az login`
` az acr login --name <acrName>`

*   With --expose-token*

`   az acr login --name <acrName> --expose-token`

**To List out, stop, delete Container in certan working default resource group. See (#Default#)**

` az container list`

` az container stop --name <container-name>`

` az container delete --name <container-name>`

* \<container-name\>: The name you assign to your container instance.
* \<acr-name\>.azurecr.io: The login server name for your ACR.
* \<image-name\>: The name of the image within your ACR.
* \<tag\>: The version tag of the image you want to use (e.g., v1.0, latest).
* \<resource-group-name\>: The name of the resource group where you want to create the ACI instance. Can remove this param if set config default group.
* \<username\>,\<password\>:

