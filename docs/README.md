# Introduction
## What is Predictive Maintenance?
Predictive Maintenance (**PdM**) is a popular application of predictive analytics that can help businesses in several industries achieve high asset utilization and savings in operational costs. 

## Predictive Maintenance for Businesses

Businesses require critical equipment to be running at peak efficiency and utilization to realize their return on capital investments. These assets could range from aircraft engines, turbines, elevators, or industrial chillers - that cost millions - down to everyday appliances like photocopiers, coffee machines, or water coolers. 

* by default, most businesses rely on *corrective maintenance*, where parts are replaces a when they fail. Corrective maintenance ensures parts are used completely (therefore not wasting component life), but costs the business in downtime, labour, and unscheduled maintenance requirements (off hours, or inconvenient locations). 
* At the next level, businesses practice *preventive maintenance, * where they determine the useful lifespan for a part, and maintain or replace it before a failure. Preventative Maintenance avoids unscheduled and catastrophic failures. But the high costs of scheduled downtime, under-utilization of the component during its lifetime, and labour remain. 
* The goal of * predictive maintenance* is to optimize the balance between corrective and preventative maintenance, by enabling *just in time* replacement of components. This approach only replaces those components when they are close to failure. By extending components lifespans (compared to preventative maintenance) and reducing unscheduled maintenance and labour costs (over corrective maintenance), businesses can gain cost savings and competitive advantage. 

## Why do businesses need PdM?
Businesses face high operational risk due to unexpected failures and having limited insight into the root cause of problems in complex systems. Some of the key business questions are:

* Detect anomalies in equipment of system performance or functionality.
* Predict whether an asset may fail soon.
* Estimate the remaining useful life of an asset. 
* Identify the main cause of failure of an asset. 
* Identify what maintenance actions need to be done, and when by, on an asset. 

### Typical goal statements from PdM are:

* Reduce operational risk of mission critical equipment. 
* Increase rate of return on assets by predicting failures before they occur. 
* Control cost of maintenance by enabling just-in-time maintenance operations. 
* Lower customer attrition, improve brand image, and lost sales. 
* Lower inventory costs by reducing inventory levels by predicting the reorder point.
* Enable just in time inventory by estimating order dates for replacement parts.
* Discover patterns connected to various maintenance problems. 
* Provide key performance indicators (KPIs) such as health scores for asset conditions. 
* Estimate remaining lifespan of assets. 
* Recommend timely maintenance activities. 


## Qualifying problems for PdM

It is important to emphasize that not all use cases or business problems can be effectively solved by PdM. There are three important qualifying criteria that need to be considered during problem selection:

* The problem must be predictive in nature—there should be a target or an outcome to predict. The problem should also have a clear path of action to prevent failures when they are detected. 
* The problem should have a record of the operational history of the equipment that contains *both good and bad outcomes*. The set of actions taken to mitigate bad outcomes should also be available as part of these records. Error reports, maintenance logs of performance degradation, repair, and replace logs are also important. 
* The recorded history should be reflected in *relevant* data that is of *sufficient* enough quality to support the use case. For more information about data relevance and sufficiency, see [Data requirements for predictive maintenance](https://docs.microsoft.com/en-us/azure/machine-learning/team-data-science-process/predictive-maintenance-playbook#data-requirements-for-predictive-maintenance).
* Finally, the business should have domain experts who have a clear understanding of the problem. They should be aware of the internal processes and practices to be able to support the analyst understand and interpret the data— and they should also be able to make the necessary changed to existing business processes to help collect the right data for the problems, if required.

If you would like develop a better undertanding of the processes involved in developing a model for PdM see (Data Science for predictive maintenance)[https://docs.microsoft.com/en-us/azure/machine-learning/team-data-science-process/predictive-maintenance-playbook#data-science-for-predictive-maintenance].


# Motivation behind this solution template

The intent behind this solution template is to showcase how to put together an end-to-end solution that demonstrates Azure ML modeling and a complete Azure infrastructure capable of supporting PdM scenarios. The components used in this template provide utility on their own and can be re-used and customized to solve other problems. 

![](img/dataFlow.png)

# Scenario

The solution deals with a hypothetical IoT-enabled manufacturing environment comprised of generalized rotational equipment, which may include pumps, turbines, gearboxes, compressors, and engines.

The machines are equipped with sensors that transmit telemetry to the cloud in real time. Maintenance logs are also available and, among other things, contain records of failure events indicating exact points in time when a machine had a critical failure of a particular type.

The objective of Predictive Maintenance is to enable businesses to practice *predicitve maintenance*—i.e. enable busiensses to predict failures far a period of time before it happens so they can be replaced. This will reduce costs incurred by replacing equipment too early as well as costs incurred from unscheduled maintenance and labour costs.

# Data acquisition

Real-world run-to-failure datasets are virtually impossible to come across due to their commercially sensitive nature—of the several publicly available synthetic datasets, none ideally fit the canonical IoT scenario in which highly irregular real-time data streams from sensors are captured and used for condition monitoring or anomaly detection. To bypass this a Jupyter Notebook run on a Data Science Virtual Machine (DSVM) is used to generate data that simulates a hypothetical IoT-enabled manufacturing environment comprised of general rotational equipment, which may include turbines and engines. The data generator is capable of producing two datasets of the same format as shown in the diagram below:

* Static seed data for model training
* Real-time telemetry data for performing end-to-end testing and validation of a complete AI-enabled IoT solution. This emulates a realistic production situation where incoming telemetry is staged over an extended period of time in storage blobs, and maintenance logs are accumulated in some other data store (exemplified as a SQL database in the diagram).

![](img/data_collection.png)

# Modeling

Having acquired an input data set, one can proceed to the modelling stage of the data science process.

![](img/modeling.png)

Modeling is an iterative process consisting of:

* Feature engineering
* Training
* Model evaluation

After selecting the best model according to the evaluation criteria, a data pipeline with scoring can be deployed to a production or production-like environment for final customer acceptance.

In this solution, modeling procedures are implemented as annotated Python 3 [Jupyter notebooks](src/Notebooks). Feature engineering is performed using Spark for the purpose of exploring and familiaring with Spark's capablities when implementing featurization in production as well as for the 
To enable scenarios with arbitrarily large input data sets (and also facilitate code/infrastructure reuse when implementing featurization in production), feature engineering is performed using Spark.

The Notebooks can run on various compute targets; the ones currently supported out-of-the-box are:

* Linux Data Science Virtual Machine (DSVM)
* Azure Databricks (feature engineering only)



