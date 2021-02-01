# Operationalizing a Machine Learning Project

## Project Overview

This project makes use of Azure to configure a cloud-based machine learning production model, deploy it, and consume it. First, an AutoML experiment was created using the specifications given and the dataset provided. Next, the model with the highest accuracy was deployed, it was the VotingEnsemble model with an accuracy of 0.92. After that, logging was enabled for the model and the documentation for the model API was created as well. Finally, the model was consumed by using the URI and the key from the gith bash console and two predictions were made as it can be seen in section 2.7 . 

In second place, an Azure pipeline was created, published and consumed. First, a notebook with the code required to submit the pipeline was uploaded to azure. After that, some specifications were modified to execute the notebook successfully. Once the pipeline was created and published, the rest API of the pipeline was used to rerun it and testing the endpoint.


## 1. Architectural Diagram

The following picture describe briefly the main steps taken to complete the project.

<img src=".\starter_files\images\project architecture.jpg">

In the next section, each step is described in detail by using screenshoots.


## 2. Key Steps

### 2.1 Dataset Registration

First of all, the Bank Marketing data was registered using the option "Create dataset", and then "From local files". The dataset can be found in the starter_files directory.

<img src=".\starter_files\images\Dataset Registration.jpg">

### 2.2 Experiment Creation and Completion

Secondly, a new automated ML experiment was created using the previously registered dataset. As an intermediate step, a compute cluster was set up in order to run it.
<img src=".\starter_files\images\Compute Cluster.jpg">

After a while, the experiment run was completed without problems.
<img src=".\starter_files\images\Experiment Completed.jpg">

### 2.3 Best Model Selection

Once the experiment run was completed, **the VotingEnsemble model** was selected as the best one from the different models generated, with an accuracy of 0.92.
<img src=".\starter_files\images\Best Model.jpg">

### 2.4 Best Model Deployment

As soon as the best model was identified, it was deployed successfully from the ML studio.
<img src=".\starter_files\images\Successful Deployment.jpg">

### 2.5 Enable Logging

Once the model is deployed, application insights should be enable. Initially, we need to download the config.json file from the best model details. After that, we can execute the provided logs.py file by using git bash.
<img src=".\starter_files\images\Logs File.jpg">
<br>Then, we can check on the Azure ML studio that application insights is enabled.
<img src=".\starter_files\images\Application Insights Enabled.jpg">
Additionally, we can review the information provided by the application insights tool.
<img src=".\starter_files\images\Application Insights Details.jpg">

### 2.6 Swagger Documentation

After deploying the model and enabling logging, the API documentation can be created using swagger. Firstly, we need to download the swagger.json file from the details of the deployed model and stored it in the swagger directory. Besides, we need to set the port as 9000 in the swagger bash file if we don't have permissions on port 80. Then, we can execute both the swagger.sh file and the serve.py file. 
<img src=".\starter_files\images\Swagger and Serve.jpg">

Next, we can test if swagger is running on localhost by using the following url http://localhost:9000.
<img src=".\starter_files\images\Swagger Localhost.jpg">

Finally, we can read the two HTTP API methods and responses available for the model by typing http://localhost:8000/swagger.json on the explore bar of the swagger UI.
<img src=".\starter_files\images\GET Request.jpg">
<img src=".\starter_files\images\Post Request 1.jpg">
<img src=".\starter_files\images\POST Request 2.jpg">

### 2.7 Consumption of the model endpoint
To interact with the deployed model, it's necessary to provide the URI and the key from the details tab of the model on Azure ML Studio. After that, all what we need to do is to execute the endpoint.py file, getting the following output:
<img src=".\starter_files\images\JSON Output.jpg">

### 2.8 Creation, consumption and publication of the model pipeline
In order to create, consume and publish the pipeline we need the previously downloaded config.json file and the notebook provided in the starter files. First, the notebook should be uploaded to Azure ML studio, and next, we need to modify the notebook with the experiment and model specifications.
<img src=".\starter_files\images\Pipeline Run.jpg">
<br> Once the pipeline is submitted, it runs for several minutes. 
<img src=".\starter_files\images\Data and Training.jpg">
<br> After a while, the pipeline run is completed without problems, along with its REST endpoint.
<img src=".\starter_files\images\Pipeline Completed.jpg">
<img src=".\starter_files\images\Pipeline Endpoint.jpg">
<br> We can test the status of the pipeline endpoint directly from the azure notebook.
<img src=".\starter_files\images\Pipeline Endpoint Status.jpg"> 
<br> Finally, by publishing the pipeline we enable the REST endpoint to rerun it with any HTTP library.
<img src=".\starter_files\images\Pipeline Rerun.jpg"> 
<img src=".\starter_files\images\Pipeline Rerun2.jpg"> 


## 3. Screen Recording

- Experiment Overview ----------->  https://youtu.be/rK20vW2XtpM
- Pipeline Overview ----------->  https://youtu.be/2s-_oR2sZNA


## 4. Standout Suggestions
- A deep data cleaning and feature engineering process before training the model could improve its prediction accuracy.
- An ONNX format would make the model more portable and easily shareable across different environments.
- The model can be deployed as a web application allowing internal and external user interaction and consumption.

