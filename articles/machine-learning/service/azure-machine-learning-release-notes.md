---
title: What's new in the release?
titleSuffix: Azure Machine Learning service
description: Learn about the latest updates to Azure Machine Learning service and the machine learning and data prep Python SDKs.
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: reference
author: hning86
ms.author: haining
ms.reviewer: j-martens
ms.date: 03/11/2019
ms.custom: seodec18
---

# Azure Machine Learning service release notes

In this article, learn about the Azure Machine Learning service releases.  For a full description of each SDK, visit the reference docs for:
+ The Azure Machine Learning's  [**main SDK for Python**](https://aka.ms/aml-sdk)
+ The Azure Machine Learning [**Data Prep SDK**](https://aka.ms/data-prep-sdk)

## 2019-03-11

### Azure Machine Learning SDK for Python v1.0.18

 + **Changes**
   + The azureml-tensorboard package replaces azureml-contrib-tensorboard.
   + With this release you can setup a user account on your managed compute cluster (amlcompute), while creating it. This can be done by simply passing these properties in the provisoning configuration. You can find more details in the [SDK reference documentation](https://docs.microsoft.com/python/api/azureml-core/azureml.core.compute.amlcompute.amlcompute?view=azure-ml-py#provisioning-configuration-vm-size-----vm-priority--dedicated---min-nodes-0--max-nodes-none--idle-seconds-before-scaledown-none--admin-username-none--admin-user-password-none--admin-user-ssh-key-none--vnet-resourcegroup-name-none--vnet-name-none--subnet-name-none--tags-none--description-none-).

### Azure Machine Learning Data Prep SDK v1.0.17

+ **New features**
  + Now supports adding two numeric columns to generate a resultant column using the expression language.

+ **Bug fixes and improvements**
  + Improved the documentation and parameter checking for random_split.
  
## 2019-02-27

### Azure Machine Learning Data Prep SDK v1.0.16

+ **Bug fix**
  + Fixed a Service Principal authentication issue that was caused by an API change.

## 2019-02-25

### Azure Machine Learning SDK for Python v1.0.17

+ **New features**

  + Azure Machine Learning now provides first class support for popular DNN framework Chainer. Using [`Chainer`](https://docs.microsoft.com/en-us/python/api/azureml-train-core/azureml.train.dnn.chainer?view=azure-ml-py) class users can easily train and deploy Chainer models.
    + Learn how to [run distributed training with ChainerMN](https://github.com/Azure/MachineLearningNotebooks/blob/master/how-to-use-azureml/training-with-deep-learning/distributed-chainer/distributed-chainer.ipynb)
    + Learn how to [run hyperparameter tuning with Chainer using HyperDrive](https://github.com/Azure/MachineLearningNotebooks/blob/master/how-to-use-azureml/training-with-deep-learning/train-hyperparameter-tune-deploy-with-chainer/train-hyperparameter-tune-deploy-with-chainer.ipynb)
  + Azure Machine Learning Pipelines added ability trigger a Pipeline run based on datastore modifications. The pipeline [schedule notebook](https://aka.ms/pl-schedule) is updated to showcase this feature.

+ **Bug fixes and improvements**
  + We have added support Azure Machine Learning Pipelines for setting the source_directory_data_store property to a desired datastore (such as a blob storage) on [RunConfigurations](https://docs.microsoft.com/en-us/python/api/azureml-core/azureml.core.runconfig.runconfiguration?view=azure-ml-py) that are supplied to the [PythonScriptStep](https://docs.microsoft.com/en-us/python/api/azureml-pipeline-steps/azureml.pipeline.steps.python_script_step.pythonscriptstep?view=azure-ml-py). By default Steps use Azure File store as the backing datastore which may run into throttling issues when a large number of steps are executed concurrently.

### Azure portal

+ **New features**
  + New drag and drop table editor experience for reports. Users can drag a column from the well to the table area where a preview of the table will be displayed. The columns can be rearranged.
  + New Logs file viewer
  + Links to experiment runs, compute, models, images and deployments from the activities tab

### Azure Machine Learning Data Prep SDK v1.0.15

+ **New features**
  + Data Prep now supports writing file streams from a dataflow. Also provides the ability to manipulate the file stream names to create new file names.
    + How-to guide: [Working With File Streams notebook](https://aka.ms/aml-data-prep-file-stream-nb)

+ **Bug fixes and improvements**
  + Improved performance of t-Digest on large data sets.
  + Data Prep now supports reading data from a DataPath.
  + One hot encoding now works on boolean and numeric columns.
  + Other miscellaneous bug fixes.

## 2019-02-11

### Azure Machine Learning SDK for Python v1.0.15

+ **New features**
  + Azure Machine Learning Pipelines added AzureBatchStep ([notebook](https://aka.ms/pl-azbatch)), HyperDriveStep ([notebook](https://aka.ms/pl-hyperdrive)) and time-based scheduling functionality ([notebook](https://aka.ms/pl-schedule)).
  +  DataTranferStep updated to work with Azure SQL Server and Azure database for PostgreSQL ([notebook](https://aka.ms/pl-data-trans)).

+ **Changes**
  + Deprecated `PublishedPipeline.get_published_pipeline` in favor of `PublishedPipeline.get`.
  + Deprecated `Schedule.get_schedule` in favor of `Schedule.get`.

### Azure Machine Learning Data Prep SDK v1.0.12

+ **New features**
  + Data Prep now supports reading from an Azure SQL database using Datastore.
 
+ **Changes**
  + Significantly improved the memory performance of certain operations on large data.
  + `read_pandas_dataframe()` now requires `temp_folder` to be specified.
  + The `name` property on `ColumnProfile` has been deprecated - use `column_name` instead.

## 2019-01-28

### Azure Machine Learning SDK for Python v1.0.10

+ **Changes**: 
  + Azure ML SDK no longer has azure-cli packages as dependency. Specifically, azure-cli-core and azure-cli-profile dependencies have been removed from azureml-core. These are the  user impacting changes:
  	+ If you are performing "az login" and then using azureml-sdk, the SDK will do the browser or device code login one more time. It won't use any credentials state created by "az login".
	+ For Azure CLI authentication, such as using "az login", use _azureml.core.authentication.AzureCliAuthentication_ class. For Azure CLI authentication, do  _pip install azure-cli_ in the Python environment where you have installed azureml-sdk.
	+ If you are doing "az login" using a service principal for automation, we recommend using _azureml.core.authentication.ServicePrincipalAuthentication_ class, as azureml-sdk won't use credentials state created by azure CLI. 

+ **Bug fixes**: This release mostly contains minor bug fixes

### Azure Machine Learning Data Prep SDK v1.0.8

+ **Bug fixes**
  + Significantly improved the performance of getting data profiles.
  + Fixed minor bugs related to error reporting.
  
### Azure portal: new features
+ New drag and drop charting experience for reports. Users can drag a column or attribute from the well to the chart area where the system will automatically select an appropriate chart type for the user based on the type of data. Users can change the chart type to other applicable types or add additional attributes.

	Supported Chart Types:
	- Line Chart
	- Histogram
	- Stacked Bar Chart
	- Box Plot
	- Scatter Plot
	- Bubble Plot
+ The portal now dynamically generates reports for experiments. When a user submits a run to an experiment, a report will automatically be generated with logged metrics and graphs to allow comparison across different runs. 

## 2019-01-14

### Azure Machine Learning SDK for Python v1.0.8

+ **Bug fixes**: This release mostly contains minor bug fixes

### Azure Machine Learning Data Prep SDK v1.0.7

+ **New features**
  + Datastore improvements (documented in [Datastore how-to-guide](https://aka.ms/aml-data-prep-datastore-nb))
    + Added ability to read from and write to Azure File Share and ADLS Datastores in scale-up.
    + When using Datastores, Data Prep now supports using service principal authentication instead of interactive authentication.
    + Added support for wasb and wasbs urls.

## 2019-01-09

### Azure Machine Learning Data Prep SDK v1.0.6

+ **Bug fixes**
  + Fixed bug with reading from public readable Azure Blob containers on Spark

## 2018-12-20 

### Azure Machine Learning SDK for Python v1.0.6
+ **Bug fixes**: This release mostly contains minor bug fixes

### Azure Machine Learning Data Prep SDK v1.0.4

+ **New features**
  + `to_bool` function now allows mismatched values to be converted to Error values. This is the new default mismatch behavior for `to_bool` and `set_column_types`, whereas the previous default behavior was to convert mismatched values to False.
  + When calling `to_pandas_dataframe`, there is a new option to interpret null/missing values in numeric columns as NaN.
  + Added ability to check the return type of some expressions to ensure type consistency and fail early.
  + You can now call `parse_json` to parse values in a column as JSON objects and expand them into multiple columns.

+ **Bug fixes**
  + Fixed a bug that crashed `set_column_types` in Python 3.5.2.
  + Fixed a bug that crashed when connecting to Datastore using an AML image.

+ **Updates**
  * [Example Notebooks](https://aka.ms/aml-data-prep-notebooks) for getting started tutorials, case studies, and how-to guides.

## 2018-12-04: General Availability

Azure Machine Learning service is now generally available.

### Azure Machine Learning Compute
With this release, we are announcing a new managed compute experience through the [Azure Machine Learning Compute](how-to-set-up-training-targets.md#amlcompute). This compute target replaces Azure Batch AI compute for Azure Machine Learning. 

This compute target:
+ Is used for model training and batch inferencing
+ Is single- to multi-node compute
+ Does the cluster management and job scheduling for the user
+ Autoscales by default
+ Support for both CPU and GPU resources 
+ Enables use of low-priority VMs for reduced cost

Azure Machine Learning Compute can be created in Python, using Azure portal, or the CLI. It must be created in the region of your workspace, and cannot be attached to any other workspace. This compute target uses a Docker container for your run, and packages your dependencies to replicate the same environment across all your nodes.

> [!Warning]
> We recommend creating a new workspace to use Azure Machine Learning Compute. There is a remote chance that users trying to create Azure Machine Learning Compute from an existing workspace might see an error. Existing compute in your workspace should continue to work unaffected.

### Azure Machine Learning SDK for Python v1.0.2
+ **Breaking changes**
  + With this release, we are removing support for creating a VM from Azure Machine Learning. You can still attach an existing cloud VM or a remote on-premises server. 
  + We are also removing support for BatchAI, all of which should be supported through Azure Machine Learning Compute now.

+ **New**
  + For machine learning pipelines:
    + [EstimatorStep](https://docs.microsoft.com/python/api/azureml-pipeline-steps/azureml.pipeline.steps.estimator_step.estimatorstep?view=azure-ml-py)
    + [HyperDriveStep](https://docs.microsoft.com/python/api/azureml-pipeline-steps/azureml.pipeline.steps.hyper_drive_step.hyperdrivestep?view=azure-ml-py)
    + [MpiStep](https://docs.microsoft.com/python/api/azureml-pipeline-steps/azureml.pipeline.steps.mpi_step.mpistep?view=azure-ml-py)


+ **Updated**
  + For machine learning pipelines:
    + [DatabricksStep](https://docs.microsoft.com/python/api/azureml-pipeline-steps/azureml.pipeline.steps.databricks_step.databricksstep?view=azure-ml-py) now accepts runconfig
    + [DataTransferStep](https://docs.microsoft.com/python/api/azureml-pipeline-steps/azureml.pipeline.steps.data_transfer_step.datatransferstep?view=azure-ml-py) now copies to and from a SQL datasource
    + Schedule functionality in SDK to create and update schedules for running published pipelines

<!--+ **Bugs fixed**-->

### Azure Machine Learning Data Prep SDK v0.5.2
+ **Breaking changes** 
  * `SummaryFunction.N` was renamed to `SummaryFunction.Count`.
  
+ **Bug Fixes**
  * Use latest AML Run Token when reading from and writing to datastores on remote runs. Previously, if the AML Run Token is updated in Python, the Data Prep runtime will not be updated with the updated AML Run Token.
  * Additional clearer error messages
  * to_spark_dataframe() will no longer crash when Spark uses `Kryo` serialization
  * Value Count Inspector can now show more than 1000 unique values
  * Random Split no longer fails if the original Dataflow doesn’t have a name  

+ **More information**
  * [Azure Machine Learning Data Prep SDK](https://aka.ms/data-prep-sdk)

### Docs and notebooks
+ ML Pipelines
  + New and updated notebooks for getting started with pipelines, batch scoping,  and style transfer examples: https://aka.ms/aml-pipeline-notebooks
  + Learn how to [create your first pipeline](how-to-create-your-first-pipeline.md)
  + Learn how to [run batch predictions using pipelines](how-to-run-batch-predictions.md)
+ Azure Machine Learning compute target
  + [Sample notebooks](https://aka.ms/aml-notebooks) are now updated to use the new managed compute.
  + [Learn about this compute](how-to-set-up-training-targets.md#amlcompute)

### Azure portal: new features
+ Create and manage [Azure Machine Learning Compute](how-to-set-up-training-targets.md#amlcompute) types in the portal.
+ Monitor quota usage and [request quota](how-to-manage-quotas.md) for Azure Machine Learning Compute.
+ View Azure Machine Learning Compute cluster status in real time.
+ Virtual network support was added for Azure Machine Learning Compute and Azure Kubernetes Service creation.
+ Rerun your published pipelines with existing parameters.
+ New [automated machine learning charts](how-to-track-experiments.md#auto) for classification models (lift, gains, calibration, feature importance chart with model explainability) and regression models (residuals and feature importance chart with model explainability). 
+ Pipelines can be viewed in Azure portal




## 2018-11-20

### Azure Machine Learning SDK for Python v0.1.80

+ **Breaking changes** 
  * *azureml.train.widgets* namespace has moved to *azureml.widgets*.
  * *azureml.core.compute.AmlCompute* deprecates the following classes - *azureml.core.compute.BatchAICompute* and *azureml.core.compute.DSVMCompute*. The latter class will be removed in subsequent releases. The AmlCompute class has an easier definition now, and simply needs a vm_size and the max_nodes, and will automatically scale your cluster from 0 to the max_nodes when a job is submitted. Our [sample notebooks](https://github.com/Azure/MachineLearningNotebooks/tree/master/training) have been updated with this information and should give you usage examples. We hope you like this simplification and lots of more exciting features to come in a later release!

### Azure Machine Learning Data Prep SDK v0.5.1 

Learn more about the Data Prep SDK by reading [reference docs](https://aka.ms/data-prep-sdk).
+ **New Features**
   * Created a new DataPrep CLI to execute DataPrep packages and view the data profile for a dataset or dataflow
   * Redesigned SetColumnType API to improve usability
   * Renamed smart_read_file to auto_read_file
   * Now includes skew and kurtosis in the Data Profile
   * Can sample with stratified sampling
   * Can read from zip files that contain CSV files
   * Can split datasets row-wise with Random Split (for example, into test-train sets)
   * Can get all the column data types from a dataflow or a data profile by calling `.dtypes`
   * Can get the row count from a dataflow or a data profile by calling `.row_count`

+ **Bug Fixes**
   * Fixed long to double conversion 
   * Fixed assert after any add column 
   * Fixed an issue with FuzzyGrouping, where it would not detect groups in some cases
   * Fixed sort function to respect multi-column sort order
   * Fixed and/or expressions to be similar to how `pandas` handles them
   * Fixed reading from dbfs path
   * Made error messages more understandable 
   * Now no longer fails when reading on remote compute target using AML token
   * Now no longer fails on Linux DSVM
   * Now no longer crashes when non-string values are in string predicates
   * Now handles assertion errors when Dataflow should fail correctly
   * Now supports dbutils mounted storage locations on Azure Databricks

## 2018-11-05

### Azure portal 
The Azure portal for the Azure Machine Learning service has the following updates:
  * A new **Pipelines** tab for published pipelines.
  * Added support for attaching an existing HDInsight cluster as a compute target.

### Azure Machine Learning SDK for Python v0.1.74

+ **Breaking changes** 
  * *Workspace.compute_targets, datastores, experiments, images, models, and *webservices* are properties instead of methods. For example, replace *Workspace.compute_targets()* with *Workspace.compute_targets*.
  * *Run.get_context* deprecates *Run.get_submitted_run*. The latter method will be removed in subsequent releases.
  * *PipelineData* class now expects a datastore object as a parameter rather than datastore_name. Similarly, *Pipeline* accepts default_datastore rather than default_datastore_name.

+ **New features**
  * The Azure Machine Learning Pipelines [sample notebook](https://github.com/Azure/MachineLearningNotebooks/tree/master/pipeline/pipeline-mpi-batch-prediction.ipynb) now uses MPI steps.
  * The RunDetails widget for Jupyter notebooks is updated to show a visualization of the pipeline.

### Azure Machine Learning Data Prep SDK v0.4.0 
 
+ **New features**
  * Type Count added to Data Profile 
  * Value Count and Histogram is now available
  * More percentiles in Data Profile
  * The Median is available in Summarize
  * Python 3.7 is now supported
  * When you save a dataflow that contains datastores to a DataPrep package, the datastore information will be persisted as part of the DataPrep package
  * Writing to datastore is now supported 
		
+ **Bug fixed**
  * 64-bit unsigned integer overflows are now handled properly on Linux
  * Fixed incorrect text label for plain text files in smart_read
  * String column type now shows up in metrics view
  * Type count now is fixed to show ValueKinds mapped to single FieldType instead of individual ones
  * Write_to_csv no longer fails when path is provided as a string
  * When using Replace, leaving “find” blank will no longer fail 

## 2018-10-12

### Azure Machine Learning SDK for Python v0.1.68

+ **New features**
  * Multi-tenant support when creating new workspace.

+ **Bugs fixed**
  * You no longer need to pin the pynacl library version when deploying web service.

### Azure Machine Learning Data Prep SDK v0.3.0

+ **New features**
  * Added method transform_partition_with_file(script_path), which allows users to pass in the path of a Python file to execute

## 2018-10-01

### Azure Machine Learning SDK for Python v0.1.65
[Version 0.1.65](https://pypi.org/project/azureml-sdk/0.1.65) includes new features, more documentation, bug fixes, and more [sample notebooks](https://aka.ms/aml-notebooks).

See [the list of known issues](resource-known-issues.md) to learn about known bugs and workarounds.

+ **Breaking changes**
  * Workspace.experiments, Workspace.models, Workspace.compute_targets, Workspace.images, Workspace.web_services return dictionary, previously returned list. See [azureml.core.Workspace](https://docs.microsoft.com/python/api/azureml-core/azureml.core.workspace(class)?view=azure-ml-py) API documentation.

  * Automated Machine Learning removed normalized mean square error from the primary metrics.

+ **HyperDrive**
  * Various HyperDrive bug fixes for Bayesian, Performance improvements for get Metrics calls. 
  * Tensorflow 1.10 upgrade from 1.9 
  * Docker image optimization for cold start. 
  * Jobs now report correct status even if they exit with error code other than 0. 
  * RunConfig attribute validation in SDK. 
  * HyperDrive run object supports cancel similar to a regular run: no need to pass any parameters. 
  * Widget improvements for maintaining state of drop-down values for distributed runs and HyperDrive runs. 
  * TensorBoard and other log files support fixed for Parameter server. 
  * Intel(R) MPI support on service side. 
  * Bugfix to parameter tuning for distributed run fix during validation in BatchAI. 
  * Context Manager now identifies the primary instance. 

+ **Azure portal experience**
  * log_table() and log_row() are supported in Run details. 
  * Automatically create graphs for tables and rows with 1, 2 or 3 numerical columns and an optional categorical column.

+ **Automated Machine Learning**
  * Improved error handling and documentation 
  * Fixed run property retrieval performance issues. 
  * Fixed continue run issue. 
  * Fixed ensembling iteration issues.
  * Fixed training hanging bug on MAC OS.
  * Downsampling macro average PR/ROC curve in custom validation scenario.
  * Removed extra index logic.
  * Removed filter from get_output API.

+ **Pipelines**
  * Added a method Pipeline.publish() to publish a pipeline directly, without requiring an execution run first.   
  * Added a method PipelineRun.get_pipeline_runs() to fetch the pipeline runs that were generated from a published pipeline.

+ **Project Brainwave**
  * Updated support for new AI models available on FPGAs.

### Azure Machine Learning Data Prep SDK v0.2.0
[Version 0.2.0](https://pypi.org/project/azureml-dataprep/0.2.0/) includes following features and bug fixes:

+ **New features**
  * Support for one-hot encoding
  * Support for quantile transform
   
+ **Bug fixed:**
  * Works with any Tornado version, no need to downgrade your Tornado version
  * Value counts for all values, not just the top three

## 2018-09 (Public preview refresh)

A new, refreshed release of Azure Machine Learning: Read more about this release: https://azure.microsoft.com/blog/what-s-new-in-azure-machine-learning-service/


## Next steps

Read the overview for [Azure Machine Learning service](../service/overview-what-is-azure-ml.md).
