# Predictive Maintenance with AI

This template showcases a complete Azure infrastructure capable of supporting Predictive Maintenance scenarios in the context of IoT remote monitoring. This repo provides reusable and customizable building blocks to enable Azure customers to solve Predictive Maintenance problems using Azure's cloud AI services.

## Main features

* Sample [Jupyter notebooks](src/Notebooks) covering feature engineering, model training, evaluation and operationalization
* Configurable and extensible [data generator](src/Notebooks/DataGeneration.ipynb) (supports static and streaming modes)
* Technical documentation
* Demo dashboard featuring IoT device management, live metrics, and prediction visualization
* Integration with Linux [Data Science Virtual Machine (DSVM)](https://docs.microsoft.com/en-us/azure/machine-learning/data-science-virtual-machine/)  and [Azure Databricks](https://azure.microsoft.com/en-us/services/databricks/)
* Compliance with [Team Data Science Process (TDSP)](https://docs.microsoft.com/en-us/azure/machine-learning/team-data-science-process/overview)

## Requirements

You will need an [Azure subscription](https://azure.microsoft.com/en-us/pricing/) to get started.

Deploying the solution will create a resource group in your subscription and populate it with the following resources:
  * [Azure Storage](https://docs.microsoft.com/en-us/azure/storage/) account
  * [Azure App Service](https://azure.microsoft.com/en-us/services/app-service/)
  * [Data Science Virtual Machine (DSVM)](https://docs.microsoft.com/en-us/azure/machine-learning/data-science-virtual-machine/)
  * [Azure Databricks](https://docs.microsoft.com/en-us/azure/azure-databricks/) workspace and cluster
  * [Azure IoT Hub](https://docs.microsoft.com/en-us/azure/iot-hub/)
  * [Azure Container Instances (ACI)](https://docs.microsoft.com/en-us/azure/container-instances/) application

## Learn More

* [Documentation](docs)
* [Azure AI guide for predictive maintenance solutions](https://docs.microsoft.com/en-us/azure/machine-learning/team-data-science-process/cortana-analytics-playbook-predictive-maintenance)
---
_This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments._
