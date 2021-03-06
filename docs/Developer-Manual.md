# Developers' Manual

This document describes implementation specifics of the solution.

## Deployment mechanism

Solution's resources are created through deployments of multiple Azure Resource Manager (ARM) [templates](../src/ARMTemplates), which are linked together by [pdm-arm.json](../src/ARMTemplates/pdm-arm.json). (Linked templates are covered in great detail in [this article](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-linked-templates).)

If you wish to customize this solution by cloning this GitHub repository, be sure to update the ```gitHubBaseUrl``` variable accordingly in the [main ARM template](../src/ARMTemplates/pdm-arm.json#L60) so that it points to your clone repository.

The ARM templates can also be reused outside of GitHub, which would require deploying them in a certain order such that resource and input/output parameter dependencies are maintained.

### Deploying your ARM Templates

#### Get tools
Let's start by making sure you have the tools you need to create and deploy templates. Install these tools on your local machine.

**Editor**
Templates are JSON files, although you can make changed by editing the templates on this repository, github was linked to a visual code to simplify making bigger chnaged and to make tracking chnages easier.

**Command-line deployment**
You also need either Azure PowerShell or Azure CLI to deploy the template. If you use Azure CLI, you must have the latest version. For the installation instructions, see:

[Install Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-az-ps)
[Install Azure CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows)
[Install Azure CLI on Linux](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux)
[Install Azure CLI on macOS](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-macos)

Azure PowerShell was used to deploy templates for this use case. 

After installing either Azure PowerShell or Azure CLI, make sure you sign in for the first time. For help, see [Sign in - PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-az-ps#sign-in)or [Sign in - Azure CLI](https://docs.microsoft.com/en-us/cli/azure/get-started-with-azure-cli#sign-in).

## Sign in to Azure
To start working with Azure PowerShell/Azure CLI, sign in with your Azure credentials.
![](img/sign-in-powerShell.PNG)
![](img/sign-in-AZ.PNG)

## Create resource group
When you deploy a template, you specify a resource group that will contain the resources. Before running the deployment command, create the resource group with either Azure CLI, Azure PowerShell as shown in the images below, or using (Azure Portal)[https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal]. 
![](img/RG-powerShell.PNG)
![](img/RG-AZ.PNG)

## Deploy ARM templates

To deploy the templates via the main template **pdm-arm.json**, use either Azure CLI or Azure PowerShell. Give a name to the deployment so you can easily identify it in the deployment history. Use the resource group you created via the commands shown above or using the (Azure Portal)[https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal] and paste the URI to the location of your **pdm-arm.json**. This needs to be copied from the *raw* view of the template. 

![](img/Deploying.PNG)
![](img/raw-URI.PNG)

### Additional provisioning activities

In addition to the ARM deployments, the solution depends on the following custom configuration activities implemented as WebJobs:

1. [Python and storage setup](../src/WebApp/App_Data/jobs/continuous/PythonAndStorageSetup), which configures Python 3.6 runtime on the Azure App Service and creates several storage tables used by the solution
2. [Databricks and simulated devices setup](../src/WebApp/App_Data/jobs/continuous/DatabricksAndSimulatedDevicesSetup), which creates a Databricks cluster used for real-time feature engineering as well as several "test" IoT devices used by the data generator.

These Web Jobs are implemented as "continuous," although, technically, they only run once. Please refer to the source code for more details.

### Web Application

The Web Jobs mentioned above, the Dashboard (Flask application) and several additional Web Job are all part of the same [Web Application](../src/WebApp), which is deployed to Azure App Service via [this ARM template](../src/ARMTemplates/demoDashboard.json). Notice that the template expects the Web Application to be packaged into a ZIP file (which can be found in the [binaries](../binaries) directry).

## Data generator

The data generator is implemented as yet another "continuous" Web Job with the name [Simulator](../src/WebApp/App_Data/jobs/continuous/Simulator). When this Web Job runs, it automatically discovers IoT devices (created during provisioning) and starts sending messages to IoT Hub. Additional simulated devices can be created manually through the solution's Dashboard.

More information on device simulation is available in the [DataGeneration.ipynb](../src/Notebooks/DataGeneration.ipynb) Jupyter notebook.

## Feature engineering and scoring pipeline

Data sent to IoT Hub by the Generator is read (using [Azure Event Hub Connector](https://github.com/Azure/azure-event-hubs-spark)) and processed by solution's [Spark Structured Streaming Job](../src/SparkJobs/Featurization) running on the Databricks cluster created during solution provisioning. This job is implemented as a Scala sbt project. It demonstrates how real-time feature engineering can be done using Spark.

Aggregated feature data is written by the Spark job into an Azure table, from where it is read by the [Scorer](../src/WebApp/App_Data/jobs/continuous/Scorer) Web Job, which defers scoring to the ML model operationalized as a Web service.

The scores (or predictions) generated by the ML model are also written into a storage table. Both feature aggregates and predictions are rendered in the solution's Dashboard as charts and tables.

## AI customization

The solution is deployed with a pre-trained AI model running as a container on Azure Container Instances (ACI).

To train and operationalize a custom AI model, please refer to the [Jupyter Notebooks](../src/Notebooks) included with the Solution. (These notebooks are also uploaded to an instance of the Linux Data Science VM (DSVM) deployed as part of the Solution. The instructions on how to access the DSVM as available in the Dashboard.)
