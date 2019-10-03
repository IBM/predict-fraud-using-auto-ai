# Fraud Prediction using Auto AI

Automation and artificial intelligence (AI) are transforming businesses and will contribute to economic growth via contributions to productivity. They will also help address challenges in areas of healthcare, technology & other areas. At the same time, these technologies will transform the nature of work and the workplace itself. In this code pattern, we will focus on building state of the art systems for churning out predictions which can be used in different scenarios. We will try to predict fraudulent transactions which we know can reduce monetary loss and risk mitigation. The same approach can be used for predicting customer churn, demand and supply forecast and others. Building predictive models require time, effort and good knowledge of algorithms to create effective systems which can predict the outcome accurately. With that being said, IBM has introduced Auto AI which will automate all the tasks involved in building predictive models for different requirements. We will get to see how Auto AI can churn out great models quickly which will save time and effort and aid in faster decision making process.

When the reader has completed this code pattern, they will understand how to :

* Quickly set up the services on cloud for model building.
* Ingest the data and initiate the Auto AI process.
* Build different models using Auto AI and evaluate the performance.
* Choose the best model and complete the deployment.
* Generate predictions using the deployed model by making ReST calls.
* Compare the process of using Auto AI and building the model manually.

# Architecture Diagram

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/architecture.png)

1. User logs into Watson Studio, creates a project and initiates an instance of Auto AI & Object Storage.
2. User uploads the data file in the CSV format to the object storage.
3. User initiates the model building process using Auto AI and create pipelines.
4. User evaluates different pipelines from Auto AI and selects the best model for deployment.
5. User generates accurate predictions by making ReST call to the deployed model.

## Included components

* [IBM Watson Studio](https://www.ibm.com/cloud/watson-studio): Analyze data using RStudio, Jupyter, and Python in a configured, collaborative environment that includes IBM value-adds, such as managed Spark.

* [IBM Auto AI](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/autoai-overview.html):The AutoAI graphical tool in Watson Studio automatically analyzes your data and generates candidate model pipelines customized for your predictive modeling problem.  

* [IBM Cloud Object Storage](https://console.bluemix.net/catalog/services/cloud-object-storage): An IBM Cloud service that provides an unstructured cloud data store to build and deliver cost effective apps and services with high reliability and fast speed to market. This code pattern uses Cloud Object Storage.


## Featured technologies

* [Artificial Intelligence](https://developer.ibm.com/technologies/artificial-intelligence/): Any system which can mimic cognitive functions that humans associate with the human mind, such as learning and problem solving.
* [Data Science](https://developer.ibm.com/code/technologies/data-science/): Systems and scientific methods to analyze structured and unstructured data in order to extract knowledge and insights.
* [Analytics](https://developer.ibm.com/code/technologies/analytics/): Analytics delivers the value of data for the enterprise.
* [Python](https://www.python.org/): Python is a programming language that lets you work more quickly and integrate your systems more effectively.

# Watch the Video

TBD

# Steps using AutoAI

Follow these steps to setup and run this code pattern using `Auto AI`.

1. [Create an account with IBM Cloud](#1-create-an-account-with-ibm-cloud)
1. [Create a new Watson Studio project](#2-create-a-new-watson-studio-project)
1. [Add Data](#3-add-data)
1. [Add Asset as Auto AI](#4-add-asset-as-auto-ai)
1. [Create and define experiment](#5-create-and-define-experiment)
1. [Import the csv file](#6-import-the-csv-file)
1. [Run experiment](#7-run-experiment)
1. [Analyze results](#8-analyze-results)
1. [Deploy to Cloud](#9-deploy-to-cloud)
1. [Model testing](#10-model-testing)




## 1. Create an account with IBM Cloud

Sign up for IBM [**Cloud**](https://console.bluemix.net/). By clicking on create a free account you will get 30 days trial account.

## 2. Create a new Watson Studio project

Sign up for IBM's [Watson Studio](http://dataplatform.ibm.com/). 

Click on New Project and select per below.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/create_prj.png)

Define the project by giving a Name and hit 'Create'.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/def_prj.png)

## 3. Add Data

[Clone this repo](https://github.com/IBM/predict-fraud-using-auto-ai)
Navigate to [data](https://github.com/IBM/predict-fraud-using-auto-ai/tree/master/data) and save the file on the disk. Review the data glossary from the data folder for more details. `Note: Citation is needed to use this dataset for any other projects.` 

Click on Assets and select Browse and add the csv file from your file system.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/add_asset.png)

## 4. Add Asset as Auto AI

Click on Add to project and select AutoAI experiment.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/sel_auto_ai.png)

`Note: The Lite account for AutoAI comes with 50 capacity units per month and AutoAI consumes 20 capacity units per hour.` 

## 5. Create and define experiment

Click on New AutoAI experiment and give a name to the experiment.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/def_exp.png)

Click on Associate a Machine Learning service instance to this project and select the Machine Learning service instance and hit reload. If you do not have Machine Learning service instance, then follow the steps on your screen to get one.

The Create button at the bottom right gets highlighted, go ahead and hit Create.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/create_exp.png)

## 6. Import the csv file

We need to import the csv file into the experiment. Note that, only csv file format is supported in AutoAI. Click on Browse or Select from project to choose the fraud_dataset.csv file to import. 

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/import_csv.png)

## 7. Run experiment

We have to select the target variable, in this case it is Fraud_Risk. Notice that Prediction Type and Optimized Metric get highlighted which tells us that we are working on Binary Classification use case and the evaluation metric is ROC (Receiver Operating Characteristics) & AUC (Area Under The Curve) which is used for classification usecases. 

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/sel_target.png)

We can click on experiment settings to adjust the holdout sample and training sample under source settings.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/sample_split.png)

We can click on prediction setting to modify the Prediction type, Positive Class & Optimized metric if required. In this case, we will leave'em as is and hit save and close.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/prediction_settings.png)

Click on `Run experiment`.

## 8. Analyze results

The AutoAI experiment has been completed in 97 seconds to generate four pipelines. `The duration of experiment depends completly on the size of the dataset`. AutoAI selects the appropriate machine learning algorithm (in the fifth stage of the process under `Model Selection`) which is best suited for the dataset. 

Each pipeline is run with different parameters, pipeline 3 is run on a sequence of HPO (hyper parameters optimization) & FE (feature engineering) where as pipeline 4 includes HPO (hyper parameters optimization), FE (feature engineering) and a combination of both. All these are done on the fly! Isn't it amazing that we just have to sit and watch while AutoAI takes care of things for us and generates awesome machine learning models!! There's very minimal intervention required to get things going and in no time we have the generated pipelines to choose from.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/generate_pipelines.png)

Click on pipeline 3 (which is ranked 1) to see the evaluation metrics on the left side.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/pipeline_3.png)

Click on model evaluation to review the performance of the model on the hold out sample and cross validation score. We can observe that our model has done very well by scoring > 95% on Recall, average Precision scores & Area under the curve scores. These scores also mean that our model is able to remember and identify fraudulent transactions with great precision.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/model_eval.png)

Click on feature importance to identify the significant features influencing the outcome. Any variable which starts with Newfeature is a variable generated on the fly by the model as part of feature engineering.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/feature_imp.png)

Click on feature transforms to understand the transformation of original features to new features. Feature engineering is one of the important factors in the model building process which has a direct impact on the overall accuracy of the model. We can observe that total features are 24 where as the original dataset had 13 variables which means 11 new features have been created by AutoAI which is one of the reasons for high accuracy of the model.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/feature_transforms.png)

After all the analysis of model performance, its time to select the model for deployment. We will go ahead and select `pipeline 3 which is Rank 1` and hit on Save as model. `We can select any of the pipelines to be saved which has highest Accuracy or any other evaluation metrics.`

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/select_model.png)

## 9. Deploy to Cloud

The saved model can be found under `Models` under the project in Watson Studio. Click on three dots on the right side below Actions and hit `Deploy.`

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/deploy_mdl.png)

In the next step, click on Add Deployment on the right side above `Actions.`

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/add_dply.png)

Define the deployment by giving a name and hit `Save.` Note that, the model will get deployed as web service as a ReST API.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/crt_dply.png)

The deployment will get initialized and the status will show as `ready` when it is complete.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/dply_ready.png)

We can click on deployed model to see three tabs, Overview, Implementation and Test. Overview tab will give all details about the deployment like name, type, status et'al. Implementation tab will give scoring endpoint and code snippets to invoke the model. Test tab will give options to test the model.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/overview.png)

## 10. Model testing

Now that we have created and deployed the model as a web service, how do we test it?? We have to click on `Test` tab which will have two options which are form and json. We can use form if we are to test one record at a time where we can give the values to each attribute manually and hit `Predict` to generate predictions. The output of 0 under `values` indicate that it is a fraudulent transaction. The output can be either 0 or 1 as per the `data glossary` provided in the data folder.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/form.png)

For predicting multiple records, we have to update the values in the json file and use the option to input json data & then hit `Predict` to generate real time predictions.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/json.png)

A sample json file has been provided for testing purpose. The format for scoring the model has to be same as given in json file. Navigate to [data-for-testing](https://github.com/IBM/predict-fraud-using-auto-ai/tree/master/data-for-testing) and save the file on the disk. Copy and paste the values in the test tab as shown above to generate predictions.

Go ahead and give it a try on different datasets as per your requirement and realize the ease of creating and deploying models quickly using `AutoAI offering by IBM.`

# Steps using Jupyter Notebook

Follow the below steps to use Jupyter Notebook for building the model. This is to compare the manual process of model building with the automated process using AutoAI.

`Create an account with IBM Cloud and then create a project in Watson Studio. Add the data as an asset. These three steps are given above in detail.`

4. [Create the notebook](#4-create-the-notebook)
5. [Insert the data as dataframe](#5-insert-the-data-as-dataframe)
6. [Run the notebook](#6-run-the-notebook)
7. [Analyze the results](#7-analyze-the-results)


## 4. Create the notebook

* Open [IBM Watson Studio](https://dataplatform.ibm.com).
* Go to the project and click on Add 
* Click on `Create notebook` to create a notebook.
* Select the `From URL` tab.
* Enter a name for the notebook.
* Optionally, enter a description for the notebook.
* Enter this Notebook URL: https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/notebook/Fraud_Detect.ipynb
* Select the runtime (8 vCPU and 32GB RAM)
* Click the `Create` button.

After the notebook is imported, click on `Not Trusted` and select the option as Yes to trust the source of the notebook.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/not_trusted.png)

`This notebook has been created to demonstrate the steps for building the model using Watson Studio platform. For other usecases, the notebook has to be created from scratch.`

## 5. Insert the data as dataframe

Click on 0010 icon at the top right side which will bring up the data assets tab.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/add.png)

Click on Insert to code dropdown and select the option Insert Pandas Dataframe.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/insert_dataframe.png)

## 6. Run the notebook

When a notebook is executed, what is actually happening is that each code cell in
the notebook is executed, in order, from top to bottom.

Each code cell is selectable and is preceded by a tag in the left margin. The tag
format is `In [x]:`. Depending on the state of the notebook, the `x` can be:

* A blank, this indicates that the cell has never been executed.
* A number, this number represents the relative order this code step was executed.
* A `*`, this indicates that the cell is currently executing.

There are several ways to execute the code cells in your notebook:

* One cell at a time.
  * Select the cell, and then press the `Play` button in the toolbar.
* Batch mode, in sequential order.
  * From the `Cell` menu bar, there are several options available. For example, you
    can `Run All` cells in your notebook, or you can `Run All Below`, that will
    start executing from the first cell under the currently selected cell, and then
    continue executing all cells that follow.

## 7. Analyze the results

After we run the cells in the notebook which includes data ingestion, data analysis, splitting the data, building the model and generating feature importance, its time to review and analyze the performance. There could be so many other activities like handling missing values, outlier management, feature engineering and hyper parameters optimization which are omitted for demo purpose.

Check the model accuracy and confusion matrix to identify precision and recall scores. We can observe that model has > 92% accuracy on test data and the Precision/Recall scores are also high.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/cf_matrix.png)

Feature importance as per the model is below. The model has highlighted some of the attributes which has high impact on the outcome. Features might or might not be fairly compared to access the impact on outcome.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/feat_imp.png)

We have used shapley values which is a very effective model evaluation technique. Shapley values calculate the importance of a feature by comparing what a model predicts with and without the feature. However, since the order in which a model sees features can affect its predictions, this is done in every possible order, so that the features are fairly compared.

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/shap.png)

We can observe that attributes like Married, Applicant Income & Credit history available are having high impact on the outcome which is to detect fraud as per shapley values. 

![](https://github.com/IBM/predict-fraud-using-auto-ai/blob/master/images/shap_ft_imp.png)

With this, we have come to the end of this code pattern where we can compare the ease of using AutoAI to build predictive models vs creating a new jupyter notebook to build and evaluate predictive models. `There's considerable reduction of time in building and deploying the models using AutoAI because it handles missing values, outliers, feature engineering & hyper parameters optimization on the fly and selects the best algorithm as per the dataset.` AI Model building process has been reduced from Days to Hours thanks to `AutoAI.` If you are a developer or a data scientist who wants to build the model quickly and deploy it for being production ready, then AutoAI is for you which will help in taking decisions faster and gives a detailed overview of the attribute relationships within the data. 

## More to come :

The integration of Auto AI and Watson Open Scale is currently in progress and will be updated at a later date.

## Related Links :

[Fraud Prediction using skewed data](https://developer.ibm.com/patterns/predicting-fraud-using-skewed-data/)

# Troubleshooting

[See DEBUGGING.md.](DEBUGGING.md)

## Citation for data :

`The dataset which is referenced in this code pattern is created and owned by R.K.Sharath Kumar, Data Scientist, IBM India Software Labs.`

# License

This code pattern is licensed under the Apache Software License, Version 2.  Separate third party code objects invoked within this code pattern are licensed by their respective providers pursuant to their own separate licenses. Contributions are subject to the Developer [Certificate of Origin, Version 1.1 (DCO)](https://developercertificate.org/) and the [Apache Software License, Version 2](http://www.apache.org/licenses/LICENSE-2.0.txt).

Check the [ASL FAQ link](http://www.apache.org/foundation/license-faq.html#WhatDoesItMEAN) for more details
