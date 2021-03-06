# Operationalizing Machine Learning
## Overview
In this project, I have worked with the Bank Marketing dataset. I have created a compute cluster for Auto ML and Compute Instance for Jupyter Notebook. Initial step is to upload bank marketing data set and register the same in Azure machine learning studio. Next I have create a Azure AutoML to automatically train the data dataset and come up with a best model and explanation. Subsequently the best model is deployed with authentication and compute type "Azure Container Instance" (ACI).Post deployment validate the application insight is not enabled as i will use azureml.core.webservice to enable application insight. As a next step use swagger.sh and serve.py to see swagger documentation fetched from swagger.json (downloaded from endpoint).Next we create the data.json by running the endpoint.py and same json file is benched mark suing the file benchmark.sh.  Once the operation is complete I have used jupyter notebook to demostrate Azure AutoML in Azure AML pipeline.This notebook starts with importing all required SDK pipeline packages,initializes a workspace , creates a experiment "Auto_ML_Experiment_1" with necessary folders.The AutoML uses the previously created compute cluster and uses the same bank marketing dataset , next it trains the dataset with "y" as the target column. We define the output of AutoMLStep using TrainingOutput. AutoML steps are ingested in pipeline and the pipeline is submitted. Next we get the best model and look for the steps. We use the bank marketing test data to test the model.Next we publish the pipeline to the workspace.We the REST url from the endpoint property of the published pipeline object and  Build an HTTP POST request to the endpoint, specifying your authentication header.  JSON payload object added with the experiment name and the batch size parameter. 

## Architecture
![image](https://user-images.githubusercontent.com/32674614/156673375-01e54d69-e9f9-4a1f-98d4-a3ff9273e7ef.png)

## Project main steps
In this project, you will following the below steps:


## Step 1: Authentication
I have usedthe lab Udacity provided and thus I have skipped this step since I am  not authorized to create a security principal. 

## Step 2: Automated ML Experiment
 In this step, I have created an experiment using Automated ML, configure a compute cluster, and use that cluster to run the experiment.
 
  - ### Dataset used [bankmarketing_train](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv)
 
  - ### FIG 1 : Creating Compute Cluster to be used by Auto ML
      ![image](https://user-images.githubusercontent.com/32674614/156851267-f4c4b0db-92f9-46cb-b63d-c6277edadb2a.png)
  - ### Fig 2: Creation of Compute Instance to be used by Jupyter Notebook
      ![image](https://user-images.githubusercontent.com/32674614/156851459-76355088-ea17-40f3-8a0f-8c592f3be32a.png)
  - ### Fig 3: Importing bankmarketing_train.csv data set , below it shows the schema
      ![image](https://user-images.githubusercontent.com/32674614/156851582-ec7b330e-ab04-4279-91dd-c1c5e1527b23.png)
  - ### Fig 4: bankmarketing_train dataset has been registered which will be ingested by AutoML and later by Jupyter NoteBook for pipeline
      ![image](https://user-images.githubusercontent.com/32674614/156851652-0f63d89d-1871-42f5-ad50-ad35c440b00b.png)
  - ### Fig 5: Creating AutoML experiment on the compute cluster and target column ???y???
      ![image](https://user-images.githubusercontent.com/32674614/156852406-409152ef-1a58-4d3a-aa5c-e7eddca80b98.png)
  - ### Fig 6: This is a Classification Experiment so selecting classification in AutoML
     ![image](https://user-images.githubusercontent.com/32674614/156852482-7bd66578-0464-4d20-93d5-431131f526c1.png)
  - ### Fig 7: Selecting the validation type to ???Auto??? with no test data selected 
     ![image](https://user-images.githubusercontent.com/32674614/156852558-24e2ced9-aef1-4f8d-8e02-207d25c21e1e.png)
  - ### Fig 8: AutoML Experiment started from past run experience it will take around 35 minutes on the selected compute cluster
     ![image](https://user-images.githubusercontent.com/32674614/156852621-30f38395-dc67-4d34-a131-8255b1a8368c.png)
  - ### Fig 9: AutoML Experiment completed
     ![image](https://user-images.githubusercontent.com/32674614/156852734-7d9b9f76-3ddb-469e-bb4b-58f2fa381a78.png)
  - ### Fig 10: Screenshot of AutoML Models (VotingEnsemble) with best model showing the explanation
     ![image](https://user-images.githubusercontent.com/32674614/156852852-a4bb5ce6-b2be-41a9-885e-86534f2996a1.png)
 
  - ### Fig 11.0: Best model metrics with accuracy of 91.563%
     ![image](https://user-images.githubusercontent.com/32674614/156853567-912aee4c-ad7c-4c67-9b3e-fc9282aaaf20.png)

  - ### Fig 11.1: Best model metrics
     ![image](https://user-images.githubusercontent.com/32674614/156853470-3c0388b4-30d1-42e1-ab73-b1af1f20bda5.png)

  - ### Fig 11.2: Best model metrics
     ![image](https://user-images.githubusercontent.com/32674614/156853518-ea50bf04-f383-4e21-82b3-666eda6aca71.png)

  - ### Fig 11.3: Best model metrics
      ![image](https://user-images.githubusercontent.com/32674614/156853437-15af37a7-dd35-44df-9d30-eef8bb93792d.png)
 

## Step 3: Deploy the Best Model
   #### Deploying the Best Model will allow to interact with the HTTP API service and interact with the model by sending data over POST requests.This can be easily done in the Azure Machine Learning Studio, which provides us with an URL to send our test data.

In this step, we deployed our trained Voting Ensemble model using Azure Container Instance (ACI), with authentication enabled.
  - ### Fig 12: Deploying the best model VotingEnsemble with ACI and enabling authentication
     ![image](https://user-images.githubusercontent.com/32674614/156852936-b73fbb93-aae5-465d-9e97-bfafc6318f1d.png)
     
  - ### Fig 13:  VotingEnsemble model deployment in progress
     ![image](https://user-images.githubusercontent.com/32674614/156853862-67203f2a-f87a-4622-9b67-de819f352195.png)
     
  - ### Fig 14:  VotingEnsemble model deployment complete   
     ![image](https://user-images.githubusercontent.com/32674614/156853934-3e97357e-3fda-4262-aa67-0fdb08db1d01.png)



## Step 4: Enable Application Insights
Now that the Best Model is deployed, enable Application Insights and retrieve logs. Although this is configurable at deploy time with a check-box, it is useful to be able   to run code that will enable it for you. (In this project I achieved it using Azure Python SDK.)

  - ### Fig 15: The model is successfully deployed, and we can access the model endpoint in the Endpoints section of Azure ML Studio.Model has REST Endpoint & Swagger URI But Application Insight Not Enabled which will enabled using logs.py
     ![image](https://user-images.githubusercontent.com/32674614/156854208-887838ed-af71-4118-aad7-fa921b4d6265.png)
     
  - ### Fig 15.1: Application Insight Not Enabled
     ![image](https://user-images.githubusercontent.com/32674614/156854277-3467e649-c072-48be-8cfc-d58a8affe05e.png)
     
  - ### Fig 16:  Checking if az and ab  is available which will be used later by scripts
     ![image](https://user-images.githubusercontent.com/32674614/156854560-3f4b63b5-dbdd-47b1-90c1-a210969b5af0.png)
     
  - ### Fig 17: Confirming all the required files are available including the configuration file config.json
     ![image](https://user-images.githubusercontent.com/32674614/156854624-e8643875-dc42-48f6-9b40-aa5bc98010f8.png)

  - Add following code to logs.py
```
     name = "automlvotingensemble"
     service = Webservice(name=name, workspace=ws)
     service.update(enable_app_insights=True)
```
 - ### Fig 18: Running logs.py to enable ???Application Insights???
    ![image](https://user-images.githubusercontent.com/32674614/156854816-17f01800-8a91-4f5e-ab54-1fb501622c2f.png)
    
 - ### Fig 19: Application Insight Enabled
    ![image](https://user-images.githubusercontent.com/32674614/156854871-5fdf8be1-ae07-48a9-9af8-4919c71debf7.png)




    
## Step 5: Swagger Documentation
 In this step, I have consume the deployed model using Swagger. Azure provides a Swagger JSON file for deployed models.
 Downloaded swagger.json and placed in the working directory.
 Port for swagger.sh changed from port 80 . I didn't had permissions for port 80 so instead I have used port 9000.
 serve.py will start a Python server on port 8000. 
Then we run the swagger.sh and serve.py files to be able to interact with the swagger instance running with the documentation for the HTTP API of the model.    
    
```
    docker run -p 9000:8080 swaggerapi/swagger-ui
```
 - ### Fig 19: Downloading swagger.json and placing it in the working directory
    ![image](https://user-images.githubusercontent.com/32674614/156855116-468245d3-d5e6-41ed-9d14-bc58c37e5e4f.png)
    
 - ### Fig 20: Executing swagger.sh
    ![image](https://user-images.githubusercontent.com/32674614/156855220-f408921a-27d8-4b58-9a0b-b2b8b838fbb8.png)
    
 - ### Fig 20.1: swagger.sh execution is updated with latest docker URI
    ![image](https://user-images.githubusercontent.com/32674614/156855323-d2b76ceb-8ee1-459f-98c0-aaffb1e20b24.png)
    
 - ### Fig 21: Executing   serve.py 
    ![image](https://user-images.githubusercontent.com/32674614/156855405-73b0ac45-1e77-4099-873e-ea207972e504.png)

 - ### Fig 22: Swagger documentation localhost:9000
    ![image](https://user-images.githubusercontent.com/32674614/156855534-6ca225e0-1397-4a08-9752-ab6b0b445ce0.png)

 - ### Fig 23: Swagger documentation for experiment on localhost:8000/swagger.json
    ![image](https://user-images.githubusercontent.com/32674614/156855556-cdb0178e-e952-4af2-b6fa-8aed5a9c9cae.png)
    
- ### Fig 24:  Swagger response
   ![image](https://user-images.githubusercontent.com/32674614/156855575-7c88ffc8-e03b-4ae2-810f-a9449b611b80.png)


   

## Step 6: Consume Model Endpoints
Once the model is deployed, i used the endpoint.py script provided to interact with the trained model. In this step, you need to run endpoint.py, before running the the script, I modifiedying both the scoring_uri and the key to match the key for your service and the URI that was generated after deployment. After running the endpoint.py a file named data.json will be generated which will be later used by benchmark.json
    
```
scoring_uri = 'http://621da048-0c8c-4b00-9d43-f57f64a53fc5.southcentralus.azurecontainer.io/score'
key ='Botc7rXPMA7Ye0iv1DCUthr6rNkOWpl7'
```

```
Two sets of data to score, so we get two results back
data = {"data":
        [
          {
            "age": 17,
            "job": "blue-collar",
            "marital": "married",
            "education": "university.degree",
            "default": "no",
            "housing": "yes",
            "loan": "yes",
            "contact": "cellular",
            "month": "may",
            "day_of_week": "mon",
            "duration": 971,
            "campaign": 1,
            "pdays": 999,
            "previous": 1,
            "poutcome": "failure",
            "emp.var.rate": -1.8,
            "cons.price.idx": 92.893,
            "cons.conf.idx": -46.2,
            "euribor3m": 1.299,     
            "nr.employed": 5099.1,      
          },
          {
            "age": 87,
            "job": "blue-collar",
            "marital": "married",
            "education": "university.degree",
            "default": "no",
            "housing": "yes",
            "loan": "yes",
            "contact": "cellular",
            "month": "may",
            "day_of_week": "mon",
            "duration": 471,
            "campaign": 1,
            "pdays": 999,
            "previous": 1,
            "poutcome": "failure",
            "emp.var.rate": -1.8,
            "cons.price.idx": 92.893,
            "cons.conf.idx": -46.2,
            "euribor3m": 1.299, 
            "nr.employed": 5099.1,   
          },
      ]
    } 
```
 Sequence of Columns of above JSON matches with the columns in CSV file and the view generated in SWAGER
 ```
 age,job,marital,education,default,housing,loan,contact,month,day_of_week,duration,campaign,pdays,previous,poutcome,emp.var.rate,cons.price.idx,cons.conf.idx,euribor3m,nr.employed,y
57,technician,married,high.school,no,no,yes,cellular,may,mon,371,1,999,1,failure,-1.8,92.89299999999999,-46.2,1.2990000000000002,5099.1,no
55,unknown,married,unknown,unknown,yes,no,telephone,may,thu,285,2,999,0,nonexistent,1.1,93.994,-36.4,4.86,5191.0,no
 ```
- ### Fig 25:   Score URI and Key match with Experiment and endpoint.py
   ![image](https://user-images.githubusercontent.com/32674614/156856200-ad672dc1-0624-4053-bae7-a2c5159f7c3b.png)


- ### Fig 26:   Executing endpoint.py it generated data.json 
  ![image](https://user-images.githubusercontent.com/32674614/156856285-20044210-680e-4b2d-be56-1ccf858f96da.png)

- ### Fig 27:  column sequence matching in endpoint.py and swager to check if json class error is because of wrong column sequence
   ![image](https://user-images.githubusercontent.com/32674614/156859201-83ad314d-711e-49ab-936f-0f14e468d220.png)


- ### Fig 28:   validating JSON on [JSONLint](https://jsonlint.com/)
![image](https://user-images.githubusercontent.com/32674614/156859296-0a861128-c821-4af7-8ecf-86aa850b12fc.png)

#### Conclusion Microsoft Azure environment didn't permint request.post  as the request.status returned 502 with gatewaay not allowed.

- ### Fig 29.0:  Executing benchmark.sh
   ![image](https://user-images.githubusercontent.com/32674614/156859498-fcf72f95-0fe6-4e8e-949c-32f9c3a4b347.png)
   
- ### Fig 29.1:  Output from  benchmark.sh
   ![image](https://user-images.githubusercontent.com/32674614/156859536-e4d13480-b30e-4208-80eb-f1235017e409.png)

## Step 7: Create, Publish and Consume a Pipeline
For this part of the project, I used Jupyter Notebook provided in the starter files. Changes made in the notebook to have the same keys, URI, dataset, cluster, and model names already created. 

 For this step, I used the aml-pipelines-with-automated-machine-learning-step Jupyter Notebook to create a PipelineI created, consumed and published the best model for the bank marketing dataset using AutoML with Python SDK. 

- ### Fig 30:  First pipeline running 
   ![image](https://user-images.githubusercontent.com/32674614/156859859-a57e43ce-aefe-4b89-8611-87c795262e68.png)

- ### Fig 31:  Pipeline running with and without SDK complete
   ![image](https://user-images.githubusercontent.com/32674614/156859906-89a2044b-8999-4716-b94b-af33f523f4a2.png)

- ### Fig  32: Published Pipeline Endpoint ???Bankmarketing Train??? in active status
   ![image](https://user-images.githubusercontent.com/32674614/156860154-341c5192-e7b7-4db9-af8c-1cf16106154b.png)

- ### Fig  33: Experiment with pipeline-rest-endpoint
   ![image](https://user-images.githubusercontent.com/32674614/156860250-61730dd9-0564-42d6-bd73-b47bbeef478a.png)

- ### Fig  34: Experiment with all runs
   ![image](https://user-images.githubusercontent.com/32674614/156860289-a36183de-2901-419c-aecc-ff1d8db8db6d.png)
   
- ### Fig  35: Experiment  section showing the  status of the pipeline   
   ![image](https://user-images.githubusercontent.com/32674614/156860346-5265309f-af7e-480f-9387-559dd7c43f09.png)
   
- ### Fig  36: pipeline-rest-endpoint run overview 
   ![image](https://user-images.githubusercontent.com/32674614/156860424-6ef0e283-3d2f-49dc-a776-192a556d95a4.png)

- ### Fig  38.0: pipeline run screen shots jupyter notebook
   ![image](https://user-images.githubusercontent.com/32674614/156860523-c2d9c808-1168-4a26-aeea-1f4dc05d64ae.png)
- ### Fig  38.1: pipeline run screen shots jupyter notebook
   ![image](https://user-images.githubusercontent.com/32674614/156860533-4797a456-12b9-485d-9feb-aabde73f12de.png)
   
- ### Fig  39:  Jupyter Notebook Confusion matrix
![image](https://user-images.githubusercontent.com/32674614/156860609-5a795834-5e46-4fdf-9233-0ef6f1bea8e8.png)

- ### Fig  40.0:  Jupyter Notebook pipeline-rest-endpoint
   ![image](https://user-images.githubusercontent.com/32674614/156860711-3febe995-3377-49d5-b5bb-a39ecdd89879.png)
   
- ### Fig  40.1:  Jupyter Notebook pipeline-rest-endpoint
![image](https://user-images.githubusercontent.com/32674614/156860724-9a54f8a7-57f1-4338-b4e5-ed0c76c820e8.png)

#
## [Screen Recording](https://youtu.be/ZVOJn034_ho)
#
## Future Improvements
![image](https://user-images.githubusercontent.com/32674614/156679005-21c713c1-183c-4fd8-ab9b-887f73418193.png)
- AutoML generated Class Balancing issue , this should be considered for future improvement.
- In order to get over the above mentioned alert multiple other techniques may be used such as resampling training data, Adaptive Synthetic,Synthetic Minority Over-sampling Technique SMOTE etc.
- Model is evaluated by its accuracy to predict. However, this is not appropriate when dealing with the imbalanced dataset , prtedicting F1 , Recall , precision etc may be misleading
- SMOTE is an Oversampling technique that allows us to generate synthetic samples for minority categories and this can help to overcome Class Imbalance.
## References:
- [how-to-configure-auto-train](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-configure-auto-train)
- [how-to-configure-auto-train](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-configure-auto-train#configure-your-experiment-settings)
- Udacity lessons
- [Preventing overfitting](https://docs.microsoft.com/en-us/azure/machine-learning/concept-manage-ml-pitfalls)
- [data guardrails](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-configure-auto-features#supported-data-guardrails)


