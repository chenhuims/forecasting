# KDD 2020 Tutorial - Building Forecasting Solutions Using Open-Source and Azure Machine Learning 

**Presenters: Chenhui Hu @Microsoft, Vanja Paunic @Microsoft**

**Contributor: Hong Ooi @Microsoft**


Time series forecasting is one of the most important topics in data science. Almost every business needs to predict the future in order to make better decisions and allocate resources more effectively. Examples of time series forecasting use cases are: financial forecasting, demand forecasting in logistics for operational planning of assets, demand forecasting for Azure resources and energy demand forecasting for campus buildings and data centers. The goal of this tutorial is to demonstrate state-of-the-art forecasting approaches to problems in retail and introduce a new repository focusing on best-practices in forecasting domain, along with a library of forecasting utilities.

## [Tutorial Overview](#Tutorial-Overview)

The tutorial will start with a quick overview of time series forecasting and traditional time series models to provide the audience with a clear background on the kind of problems that we aim to solve. We will also briefly explore the dataset to be used in all exercises.
 
Next, we will run through several exercises to solve a forecasting problem in retail. We will start with a traditional statistical approach, e.g. ARIMA, using an auto-arima function in python. Next we will cover machine-learning based approach to forecasting, and cover various ways to featurize the time series dataset, then train a LightGBM model. Finally, we will describe a deep-neural-net based approach, namely Dilated CNN, and train a Dilated CNN model on our data. Using LightGBM and Dilated CNN - two efficient and state-of-the-art models, we can train the models quickly and achieve very high forecasting accuracies. 

In the last part of the tutorial, we will cover an example of hyper-parameter tuning in forecasting, and use HyperDrive in Azure Machine Learning service to achieve the task. As a part of this exercise, we will also demonstrate how to deploy the trained model to Azure Container Instance (ACI), and test the deployed service.
 
The repository also contains best-practice implementations in R language. Time permitting, we will cover common approaches to solving forecasting problems in R, ranging from simple regression models to more complex one, such as a Prophet package in R.


## [Tutorial Outline](#Tutorial-Outline)

1. [Tutorial introduction](#Tutorial-Overview)
    * Tutorial goals and agenda
    * [Target audience](#Target-Audience)
    * [Technical set-up](#Getting-Started-in-Python)

2. Introduction to time series forecasting
    * Intro to times series forecasting
    * [Overview of the public Forecasting Best-Practices repository](#Forecasting-Best-Practices)
    * [Retail data exploration and preparation](examples/grocery_sales/python/01_prepare_data/)

3.	[Hands-on: statistical time series forecasting](examples/grocery_sales/python/00_quick_start/autoarima_single_round.ipynb)
    * Data preparation
    * Time series cross-validation
    * Training a forecasting model using Auto-Arima
    * Forecasting evaluation

4.	[Hands-on: LightGBM](examples/grocery_sales/python/00_quick_start/lightgbm_single_round.ipynb)
    * Time series data featurization
    * Training a LightGBM model
   
5.	[Hyper-parameter tuning](examples/grocery_sales/python/03_model_tune_deploy/azure_hyperdrive_lightgbm.ipynb)
    * How to do hyper-parameter tuning using Azure ML hyperdrive
    * Model deployment to Azure Container Instance

6.	[Hands-on: Dilated CNN](examples/grocery_sales/python/02_model/dilatedcnn_multi_round.ipynb)
    * Training and evaluation of a Dilated CNN model

7.	(Optional) [Best-practice forecasting approaches in R](examples/grocery_sales/R)

8.	Conclusion and Q&A


## [Forecasting Best Practices](#Forecasting-Best-Practices)

This repository provides examples and best practice guidelines for building forecasting solutions. The goal of this repository is to build a comprehensive set of tools and examples that leverage recent advances in forecasting algorithms to build solutions and operationalize them. Rather than creating implementations from scratch, we draw from existing state-of-the-art libraries and build additional utilities around processing and featurizing the data, optimizing and evaluating models, and scaling up to the cloud. 

The examples and best practices are provided as [Python Jupyter notebooks and R markdown files](examples) and [a library of utility functions](fclib). We hope that these examples and utilities can significantly reduce the “time to market” by simplifying the experience from defining the business problem to the development of solutions by orders of magnitude. In addition, the example notebooks would serve as guidelines and showcase best practices and usage of the tools in a wide variety of languages.


## [Repository Content](#Repository-Content)

The following is a summary of models and methods for developing forecasting solutions covered in this repository. The [examples](examples) are organized according to use cases. Currently, we focus on a retail sales forecasting use case as it is widely used in [assortment planning](https://repository.upenn.edu/cgi/viewcontent.cgi?article=1569&context=edissertations), [inventory optimization](https://en.wikipedia.org/wiki/Inventory_optimization), and [price optimization](https://en.wikipedia.org/wiki/Price_optimization). To enable high-throughput forecasting scenarios, we have included examples for forecasting multiple time series with distributed training techniques such as Ray in Python, parallel package in R, and multi-threading in LightGBM. Note that html links are provided next to R examples for best viewing experience when reading this document on our [`github.io`](https://microsoft.github.io/forecasting/) page.

| Model                                                                                             | Language | Description                                                                                                 |
|---------------------------------------------------------------------------------------------------|----------|-------------------------------------------------------------------------------------------------------------|
| [Auto ARIMA](examples/grocery_sales/python/00_quick_start/autoarima_single_round.ipynb)           | Python   | Auto Regressive Integrated Moving Average (ARIMA) model that is automatically selected                      |
| [Linear Regression](examples/grocery_sales/python/00_quick_start/azure_automl_single_round.ipynb) | Python   | Linear regression model trained on lagged features of the target variable and external features             |
| [LightGBM](examples/grocery_sales/python/00_quick_start/lightgbm_single_round.ipynb)              | Python   | Gradient boosting decision tree implemented with LightGBM package for high accuracy and fast speed          |
| [DilatedCNN](examples/grocery_sales/python/02_model/dilatedcnn_multi_round.ipynb)                 | Python   | Dilated Convolutional Neural Network that captures long-range temporal flow with dilated causal connections |
| [Mean Forecast](examples/grocery_sales/R/02_basic_models.Rmd) [(.html)](examples/grocery_sales/R/02_basic_models.nb.html)                                | R        | Simple forecasting method based on historical mean                                                          |
| [ARIMA](examples/grocery_sales/R/02a_reg_models.Rmd) [(.html)](examples/grocery_sales/R/02a_reg_models.nb.html)                                              | R        | ARIMA model without or with external features                                                               |
| [ETS](examples/grocery_sales/R/02_basic_models.Rmd) [(.html)](examples/grocery_sales/R/02_basic_models.nb.html)                                              | R        | Exponential Smoothing algorithm with additive errors                                                        |
| [Prophet](examples/grocery_sales/R/02b_prophet_models.Rmd) [(.html)](examples/grocery_sales/R/02b_prophet_models.nb.html)                                       | R        | Automated forecasting procedure based on an additive model with non-linear trends                           |

The repository also comes with AzureML-themed notebooks and best practices recipes to accelerate the development of scalable, production-grade forecasting solutions on Azure. In particular, we have the following examples for forecasting with Azure AutoML as well as tuning and deploying a forecasting model on Azure.

| Method                                                                                                    | Language | Description                                                                                                |
|-----------------------------------------------------------------------------------------------------------|----------|------------------------------------------------------------------------------------------------------------|
| [Azure AutoML](examples/grocery_sales/python/00_quick_start/azure_automl_single_round.ipynb)              | Python   | AzureML service that automates model development process and identifies the best machine learning pipeline |
| [HyperDrive](examples/grocery_sales/python/03_model_tune_deploy/azure_hyperdrive_lightgbm.ipynb)          | Python   | AzureML service for tuning hyperparameters of machine learning models in parallel on cloud                 |
| [AzureML Web Service](examples/grocery_sales/python/03_model_tune_deploy/azure_hyperdrive_lightgbm.ipynb) | Python   | AzureML service for deploying a model as a web service on Azure Container Instances                        |


## [Getting Started in Python](#Getting-Started-in-Python)

To quickly get started with the repository on your local machine, use the following commands.

1. Install Anaconda with Python >= 3.6. [Miniconda](https://conda.io/miniconda.html) is a quick way to get started.

2. Clone the repository
    ```
    git clone https://github.com/microsoft/forecasting
    cd forecasting/
    ```

3. Run setup scripts to create conda environment. Please execute one of the following commands from the root of Forecasting repo based on your operating system.

    - Linux
    ```
    ./tools/environment_setup.sh
    ```

    - Windows
    ```
    tools\environment_setup.bat
    ```

    Note that for Windows you need to run the batch script from Anaconda Prompt. The script creates a conda environment `forecasting_env` and installs the forecasting utility library `fclib`.

4. Activate conda environment and start the Jupyter notebook server
    ```
    conda activate forecasting_env
    jupyter notebook
    ```
    
5. Run the [LightGBM single-round](examples/grocery_sales/python/00_quick_start/lightgbm_single_round.ipynb) notebook under the `00_quick_start` folder. Make sure that the selected Jupyter kernel is `forecasting_env`.

If you have any issues with the above setup, or want to find more detailed instructions on how to set up your environment and run examples provided in the repository, on local or a remote machine, please navigate to the [Setup Guide](./docs/SETUP.md).

## [Getting Started in R](#Getting-Started-in-R)

We assume you already have R installed on your machine. If not, simply follow the [instructions on CRAN](https://cloud.r-project.org/) to download and install R.

The recommended editor is [RStudio](https://rstudio.com), which supports interactive editing and previewing of R notebooks. However, you can use any editor or IDE that supports RMarkdown. In particular, [Visual Studio Code](https://code.visualstudio.com) with the [R extension](https://marketplace.visualstudio.com/items?itemName=Ikuyadeu.r) can be used to edit and render the notebook files. The rendered `.nb.html` files can be viewed in any modern web browser.

The examples use the [Tidyverts](https://tidyverts.org) family of packages, which is a modern framework for time series analysis that builds on the widely-used [Tidyverse](https://tidyverse.org) family. The Tidyverts framework is still under active development, so it's recommended that you update your packages regularly to get the latest bug fixes and features.

## [Target Audience](#Target-Audience)
Our target audience for this repository includes data scientists and machine learning engineers with varying levels of knowledge in forecasting as our content is source-only and targets custom machine learning modelling. The utilities and examples provided are intended to be solution accelerators for real-world forecasting problems.

## [Contributing](#Contributing)
We hope that the open source community would contribute to the content and bring in the latest SOTA algorithm. This project welcomes contributions and suggestions. Before contributing, please see our [Contributing Guide](CONTRIBUTING.md).

## [Reference](#Reference)

The following is a list of related repositories that you may find helpful.

|                                                                                                            |                                                                                                 |
|------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
| [Deep Learning for Time Series Forecasting](https://github.com/Azure/DeepLearningForTimeSeriesForecasting) | A collection of examples for using deep neural networks for time series forecasting with Keras. |
| [Microsoft AI Github](https://github.com/microsoft/ai)                                                     | Find other Best Practice projects, and Azure AI designed patterns in our central repository.    |



## [Build Status](#Build-Status)

| Build         | Branch  | Status  |
| -  | -  | - |
| **Linux CPU** | master  | [![Build Status](https://dev.azure.com/best-practices/forecasting/_apis/build/status/cpu_unit_tests_linux?branchName=master)](https://dev.azure.com/best-practices/forecasting/_build/latest?definitionId=128&branchName=master)   |
| **Linux CPU** | staging | [![Build Status](https://dev.azure.com/best-practices/forecasting/_apis/build/status/cpu_unit_tests_linux?branchName=staging)](https://dev.azure.com/best-practices/forecasting/_build/latest?definitionId=128&branchName=staging) |
