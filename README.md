# Deploy an Azure Function using an ARM template

The NwNSGGlowLogs branch contains a working version of the deployment template, tailored for a real version of a function that transmits Azure Network Watcher NSG Flow Logs to Arcsight.  

[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fsebastus%2FAzureFunctionDeployment%2FNwNSGFlowLogs%2FazureDeploy.json)

## Overview

The steps to fully implement the Azure Network Watcher NSG Flow Logs Connector are:  
* Gather the settings below.
* Click the "Deploy to Azure" button below.
* Authenticate to the Azure Portal (if necessary)
* Fill in the form with the setting values
* Wait a few minutes for the function to be created and deployed
* In the UI of your monitoring tool (ArcSight?), query for the records that are being sent over.

## Settings

* AppName                     - this is the name of the function app. In the Azure Portal, this is the name that will appear in the list of resources.
* appServicePlanTier          - "Free", "Shared", "Basic", "Standard", "Premium", "PremiumV2"
* appServicePlanName          - depends on tier, for full details see "Choose your pricing tier" in the portal on an App service plan "Scale up" applet.
   Example: For standard tier, "S1", "S2", "S3" are options for plan name
* appServicePlanCapacity      - how many instances do you want to set for the upper limit?
   Example: For standard tier, S2, set a value from 1 to 10
* githubRepoURL                     - this is the URL of the repo that contains the function app source.  
   Example: ```https://github.com/microsoft/AzureNetworkWatcherNSGFlowLogsConnector```
* githubRepoBranch                  - this is the name of the branch containing the code you want to deploy.  
   Example: ```master```
* blobContainerName           - the name of the blob container from which NSG blobs are to be acquired, normally doesn't change
   Example: ```insights-logs-networksecuritygroupflowevent```
* nsgSourceDataAccount              - indirection pointer to storage account reference
   Example: ```nsgSourceDataConnection1```
* nsgSourceDataConnection1    - a storage account connection string
   Example: ```DefaultEndpointsProtocol=https;AccountName=yyy;AccountKey=xxx;EndpointSuffix=core.windows.net```
* cefLogAccount               - a storage account connection string - account into which trace logs of incoming json and outgoing cef are dropped
   Example: ```DefaultEndpointsProtocol=https;AccountName=yyy;AccountKey=xxx;EndpointSuffix=core.windows.net```
* outputBinding               - Points to the destination service - the service that will receive the NSG flow log data. There may be other output bindings in future.
   Example: ```arcsight```
* arcsightAddress  
   Example: ```192.168.1.1```
* arcsightPort                - TCP port to connect to on destination server
   Example: ```1514```
