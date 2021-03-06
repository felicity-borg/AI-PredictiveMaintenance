# Predictive Maintenance with AI

The purpose of this template is to develop a complete Azure infrastructure capable of supporting Predictive Maintenance scenarios in the context of IoT remote monitoring. This repo provides reusable building blocks that can be customized to solve customers' Predictive Maintenance problems using Azure's cloud AI services.

## Main Features

* Sample [Jupyter notebooks](src/Notebooks) covering feature engineering, model training, evaluation and operationalization
* Configurable and extensible [data generator](src/Notebooks/DataGeneration.ipynb) (supports static and streaming modes)
* Technical documentation
* Demo dashboard featuring IoT device management, live metrics, and prediction visualization
* Integration with Linux [Data Science Virtual Machine (DSVM)](https://docs.microsoft.com/en-us/azure/machine-learning/data-science-virtual-machine/)  and [Azure Databricks](https://azure.microsoft.com/en-us/services/databricks/)
* Compliance with [Team Data Science Process (TDSP)](https://docs.microsoft.com/en-us/azure/machine-learning/team-data-science-process/overview)

## Required Azure Resources

You will need an [Azure subscription](https://azure.microsoft.com/en-us/pricing/) to get started.

Deploying the solution will create a resource group in your subscription and populate it with the following resources:
  * [Azure Storage](https://docs.microsoft.com/en-us/azure/storage/) account
  * [Azure App Service](https://azure.microsoft.com/en-us/services/app-service/)
  * [Data Science Virtual Machine (DSVM)](https://docs.microsoft.com/en-us/azure/machine-learning/data-science-virtual-machine/)
  * [Azure Databricks](https://docs.microsoft.com/en-us/azure/azure-databricks/) workspace and cluster
  * [Azure IoT Hub](https://docs.microsoft.com/en-us/azure/iot-hub/)
  * [Azure Container Instances (ACI)](https://docs.microsoft.com/en-us/azure/container-instances/) application
  
  For the purpose of this use case the resource group was created in West US 2 as there is an issue with deploying resources in Europe when using the DSVM, for more info see  [here](https://github.com/Azure/AI-PredictiveMaintenance/issues/150).
  The DSVM was used for this solution to generate the data; when customising this solution for a use case, a DSVM should not be required and resource groups can be created in     more feasible locations. 
  
 **Note** When creating a username and password for the DSVM use lowercase letters in your username to avoid the `500 Error` when accessing the DSVM using Jupyter Notebooks. The `500 error` is  occurs when you have used upper case letter in your `username` and is a known interaction between Jupyter Hub and the PAMAuthenticator it uses. For more info see [here](https://docs.microsoft.com/en-us/azure/machine-learning/data-science-virtual-machine/dsvm-ubuntu-intro#create-your-data-science-virtual-machine-for-linux).

## Learn More

* [Documentation](docs)
* [Azure AI guide for predictive maintenance solutions](https://docs.microsoft.com/en-us/azure/machine-learning/team-data-science-process/cortana-analytics-playbook-predictive-maintenance)
---
