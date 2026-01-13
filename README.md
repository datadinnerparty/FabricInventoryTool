# What is the Fabric Inventory Tool?
The Fabric Inventory Tool collects metadata about all items in all workspaces in a client fabric environment, and shows reports of that inventory, including counts over time.

The purpose is to help organizations understand what fabric items they have, when they are created, and how long they live.

# Prerequisites
* You must have a Fabric Workspace, capable of running notebooks and creating lakehouses
* The user that owns the notebook must have permissions to the desired workspaced where the lakehouse resides.
* The user that owns the notebook MUST have permissions to write to the lakehouse
* You must have a service principal created.  You'll need the tenant_id, client_id and secret
* You must have a configured keyvault, with the tenantid, clientid and secret as separate keys in the same keyvault
* the service principal and the notebook owner must have at least read access to the keyvault
* the service principal must be within a security group
* the security group that contains the service principale must be enabled ot use the fabric apis, and the fabric admin apis.
* fabric apis (including admin apis) must be enabled in the tenant settings.

Specific directions for configuring the Service Principal and Key Vault are included in the [Prerequisite Document](Prerequisites - Fabric Inventory Tool.docx) file

# Which Files do I Need?
There are 3 files needed to install/use this tool, located in the 'files' folder:
* FabricInventoryTool_Setup - a notebook that you need to run only once to setup the lakehouse and tables needed.
* FabricInventoryTool_Process - a notebook that you can schedule to run as often as you like, that reads in the inventory metadata
* FabricInventory.pbit - A Power BI Report template, that you'll point to your lakehouse (created in the Setup notebook)
![Parameters dialog](/images/pbiparameters.png)

If you want to contribute to this project, create a branch and pull request here in GitHub (approval required for PR).

# What does the Model Catalog Do?
* Queries the metadata of all workspaces and tracks what objects exist. 
* Provides a templated, parameterized report for quick and easy deployment

![Measure description](/images/overview.png)


# Metadata Included in the Model Catalog
* Item Name - the defined name of the Fabric item
* Item Id - the GUID of the item
* Workspace - the workspace where the item lives
* Date - the date the item was scanned by the tool


# Refreshing the published Fabric Inventory Tool
The FabricInventoryTool_Process notebook can be scheduled directly within the workspace, or included in a pipeline.
The Power BI Semantic Model will be triggered by the notebook, although you can also configure an auto refresh as you would any other Power BI model.


