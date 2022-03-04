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
  - ### Fig 5: Creating AutoML experiment on the compute cluster and target column “y”
      ![image](https://user-images.githubusercontent.com/32674614/156852406-409152ef-1a58-4d3a-aa5c-e7eddca80b98.png)
  - ### Fig 6: This is a Classification Experiment so selecting classification in AutoML
     ![image](https://user-images.githubusercontent.com/32674614/156852482-7bd66578-0464-4d20-93d5-431131f526c1.png)
  - ### Fig 7: Selecting the validation type to “Auto” with no test data selected 
     ![image](https://user-images.githubusercontent.com/32674614/156852558-24e2ced9-aef1-4f8d-8e02-207d25c21e1e.png)
  - ### Fig 8: AutoML Experiment started from past run experience it will take around 35 minutes on the selected compute cluster
     ![image](https://user-images.githubusercontent.com/32674614/156852621-30f38395-dc67-4d34-a131-8255b1a8368c.png)
  - ### Fig 9: AutoML Experiment completed
     ![image](https://user-images.githubusercontent.com/32674614/156852734-7d9b9f76-3ddb-469e-bb4b-58f2fa381a78.png)
  - ### Fig 10: Screenshot of AutoML Models with best model showing the explanation
     ![image](https://user-images.githubusercontent.com/32674614/156852852-a4bb5ce6-b2be-41a9-885e-86534f2996a1.png)
 
 

## Step 3: Deploy the Best Model
   #### Deploying the Best Model will allow to interact with the HTTP API service and interact with the model by sending data over POST requests.
   #### This can be easily done in the Azure Machine Learning Studio, which provides us with an URL to send our test data.

In this step, we deployed our trained Voting Ensemble model using Azure Container Instance (ACI), with authentication enabled.
  - ### Fig 10: Deploying the best model VotingEnsemble with ACI and enabling authentication
     ![image](https://user-images.githubusercontent.com/32674614/156852936-b73fbb93-aae5-465d-9e97-bfafc6318f1d.png)
     
     
#### The model is successfully deployed, and we can access the model endpoint in the Endpoints section of Azure ML Studio.
  - ![image](https://user-images.githubusercontent.com/32674614/156615547-106bbe1a-9dfb-45c1-bc1e-53d3b053ef46.png)
#### Model has transitioned completely and in Healthy condition
  - ![image](https://user-images.githubusercontent.com/32674614/156615604-7691bd5f-7747-4693-96ab-d6fa7bde0a60.png)
#### Model has REST Endpoint & Swagger URI But Application Insight Not Enabled which will enabled using logs.py
  - ![image](https://user-images.githubusercontent.com/32674614/156615644-0c0a633b-2199-4325-8c73-d99cb92d8473.png)

## Step 4: Enable Application Insights
Now that the Best Model is deployed, enable Application Insights and retrieve logs. Although this is configurable at deploy time with a check-box, it is useful to be able   to run code that will enable it for you. (In this project I achieved it using Azure Python SDK.)
     - Add following code to logs.py
```
     name = "automlvotingensemble"
     service = Webservice(name=name, workspace=ws)
     service.update(enable_app_insights=True)
```
### Checking if az is installed
  - ![image](https://user-images.githubusercontent.com/32674614/156616882-fddebbe7-4f0f-41d5-b96d-56738ddb9735.png)
### updated logs.py to enable enable_app_insights=True
  - ![image](https://user-images.githubusercontent.com/32674614/156616942-4c73f507-e920-4368-9178-ca61b11446dc.png)
### executing logs.py
  - ![image](https://user-images.githubusercontent.com/32674614/156617033-7ef7cc9e-0075-40c1-bb3d-6a3633a002dd.png)
### validating credentials
  - ![image](https://user-images.githubusercontent.com/32674614/156617126-0ac3a800-7ef8-4084-a170-1da325511217.png)
### After validating credentials logs.py execution completes
  - ![image](https://user-images.githubusercontent.com/32674614/156617216-b27c7be7-3cbe-4120-9f07-85906de3eae6.png)
### Experiment still in Transition State
  - ![image](https://user-images.githubusercontent.com/32674614/156617320-2defd71d-1737-4a2a-bcf5-f757b32660c2.png)
  - ![image](https://user-images.githubusercontent.com/32674614/156617383-0a1ad4a9-987d-4cdc-a42e-efd2c547492c.png)
### Transition complete and deployment is in healthy state  
  - ![image](https://user-images.githubusercontent.com/32674614/156617445-cbc6bf1b-d82e-4848-a023-8e4f16aee8f8.png)
### Enabled Application Insights 
  - ![image](https://user-images.githubusercontent.com/32674614/156617491-a957cfd2-579d-4ad7-84a0-379a760dca03.png)

    
## Step 5: Swagger Documentation
 In this step, I have consume the deployed model using Swagger. Azure provides a Swagger JSON file for deployed models.
 Downloaded swagger.json and placed in the working directory.
 Port for swagger.sh changed from port 80 . I didn't had permissions for port 80 so instead I have used port 9000.
 serve.py will start a Python server on port 8000. 
Then we run the swagger.sh and serve.py files to be able to interact with the swagger instance running with the documentation for the HTTP API of the model.    
    
```
    docker run -p 9000:8080 swaggerapi/swagger-ui
```
### swagger.json placed in working directory     
   - ![image](https://user-images.githubusercontent.com/32674614/156668636-5479aacb-e63a-488f-8362-49ec1a001ffb.png)
### Executing swagger.sh   
   - ![image](https://user-images.githubusercontent.com/32674614/156668718-d510a548-c9b5-4953-897a-2c70ec04a71a.png)
###  swagger.sh   ready
   - ![image](https://user-images.githubusercontent.com/32674614/156668761-7910da74-bf5f-415a-8542-244cb464c9a9.png)
###  executing   serve.py 
   - ![image](https://user-images.githubusercontent.com/32674614/156668794-f31bc130-f93f-47a4-815f-fbbb9f0d4006.png)
###  This is the default Swagger documentation localhost:9000    
   - ![image](https://user-images.githubusercontent.com/32674614/156668813-f151abe1-c05f-4f88-99d1-1a537e3e371a.png)
###  Opening up experiment's swagger localhost:8000/swagger.json  
   - ![image](https://user-images.githubusercontent.com/32674614/156668838-b4ad761e-2efa-42b2-9fc4-67820121b114.png)
###  Output of swagger documentation localhost:8000/swagger.json   - 
   - ![image](https://user-images.githubusercontent.com/32674614/156668863-b9946be4-9265-4aee-a34b-9d0a76709a94.png)
   - ![image](https://user-images.githubusercontent.com/32674614/156668889-76315eb1-33e9-452d-bf2a-f7aca576a3a1.png)
   

## Step 6: Consume Model Endpoints
Once the model is deployed, i used the endpoint.py script provided to interact with the trained model. In this step, you need to runBefore running the the script, I modifiedying both the scoring_uri and the key to match the key for your service and the URI that was generated after deployment.
    
```
scoring_uri = 'http://e70d6ee6-73d9-43fa-aeed-f0c281d6a214.southcentralus.azurecontainer.io/score'
key ='sVpcS6jiegm8sEGvdXyXT4paPpdzivxK'
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
 ### Score URI and Key match with Experiment and endpoint.py
 ![image](https://user-images.githubusercontent.com/32674614/156670161-ba0e0ed9-15a0-40b5-803c-c919e2d502fd.png)

### endpoint.py errors out 
![image](https://user-images.githubusercontent.com/32674614/156670284-e124b526-ba6f-46c6-a68b-774e7a14b457.png)

### column sequence matching in endpoint.py and swager
![image](https://user-images.githubusercontent.com/32674614/156670365-fa6454ec-042b-4468-a28f-919852acc12c.png)

### column sequence in dataset
![image](https://user-images.githubusercontent.com/32674614/156670423-fd0e1a22-27fe-4f14-a3d4-e6e4f1ce2119.png)
![image](https://user-images.githubusercontent.com/32674614/156670453-33e355b7-6adc-4346-b6b5-423445f74c85.png)

### column data type in dataset
![image](https://user-images.githubusercontent.com/32674614/156670532-efce8152-0b80-4dc9-a8c5-b8b823c35684.png)
![image](https://user-images.githubusercontent.com/32674614/156670605-a750f252-567d-48b2-98eb-aed077b96454.png)
![image](https://user-images.githubusercontent.com/32674614/156670665-1bda5e2b-b927-4607-af59-f12731f8e8ce.png)
![image](https://user-images.githubusercontent.com/32674614/156670691-d6219125-1655-47d4-adee-c290ffd64735.png)
![image](https://user-images.githubusercontent.com/32674614/156670727-56a8c39d-4991-4ccc-85c8-e28d5a657fa8.png)
![image](https://user-images.githubusercontent.com/32674614/156670782-d2168a52-7ff9-43af-b69f-c3e3f89a5a35.png)

### validating JSON on [JSONLint](https://jsonlint.com/)
![image](https://user-images.githubusercontent.com/32674614/156670845-64c01647-fad9-4e29-9e5c-72445ee04005.png)

### testing same JSON data in experiment (I get correct result)
![image](https://user-images.githubusercontent.com/32674614/156671309-048e8553-dfdd-4a4a-85b1-ab4ac30e2810.png)
![image](https://user-images.githubusercontent.com/32674614/156671321-3755b471-ec8e-4009-a2f2-03f149fdb947.png)
![image](https://user-images.githubusercontent.com/32674614/156671342-9fbc9ef1-3d53-4ace-a04d-c4270aaa7b3f.png)

### Validating Azure not permiting requests.post( ..to my user,resp.status_code return 502, access denied by gateway 
![image](https://user-images.githubusercontent.com/32674614/156671539-628cff21-1075-4209-86d2-64696e91e92c.png)

## Conclusion Microsoft Azure environment didn't permint request.post to my use.

### running benchmark.sh
![image](https://user-images.githubusercontent.com/32674614/156672014-ab4fbb52-fdef-4cb8-baa9-5a1b3236a0d7.png)
![image](https://user-images.githubusercontent.com/32674614/156672048-1af9973a-19ec-41b7-b4e1-5dc1bee8c70f.png)


## Step 7: Create, Publish and Consume a Pipeline
For this part of the project, I used Jupyter Notebook provided in the starter files. Changes made in the notebook to have the same keys, URI, dataset, cluster, and model names already created. 

 - ![image](https://user-images.githubusercontent.com/32674614/156672213-e676fb08-5a82-422c-9c71-812bfc320373.png)
 - 
#### For this step, I used the aml-pipelines-with-automated-machine-learning-step Jupyter Notebook to create a PipelineI created, consumed and published the best model for the bank marketing dataset using AutoML with Python SDK. 
 - ![image](https://user-images.githubusercontent.com/32674614/156672267-cd5540dc-38bc-43e1-b90e-ad985b18ae9b.png)
#### pipeline running
 - ![image](https://user-images.githubusercontent.com/32674614/156672294-21ce6c6b-9499-4421-aaa9-5b8b56fefcb4.png)
#### notebook shows pipeline completed
 - ![image](https://user-images.githubusercontent.com/32674614/156672318-567545ac-0769-48fa-889b-f28cae372746.png)
#### automl_bank_marketing_experiment completed (pipeline run overview)
 - ![image](https://user-images.githubusercontent.com/32674614/156672343-f32f4ea4-689c-498f-a973-da8d616ac578.png)
#### pipeline run overview
 - ![image](https://user-images.githubusercontent.com/32674614/156672362-5ab779f2-3ad4-499f-9cff-793289c64338.png)
#### VotingEnsemble found to be the best model 
 - ![image](https://user-images.githubusercontent.com/32674614/156672404-c556e165-a6f7-4fa6-9997-043aaaed1db5.png)
#### VotingEnsemble metrics  
 - ![image](https://user-images.githubusercontent.com/32674614/156672421-8e4ef8ac-a7c1-4e72-a381-df948d11edb5.png)
 - ![image](https://user-images.githubusercontent.com/32674614/156672446-b98a6910-fbc0-4a1f-bc6a-cb627ea87c36.png)
 - ![image](https://user-images.githubusercontent.com/32674614/156672472-90d57039-3c6c-409e-8a5a-76e9bdc43426.png)
#### Notebook Screen Details   
 - ![image](https://user-images.githubusercontent.com/32674614/156672491-2337ef08-30c1-4942-9c8f-3bbdcf396061.png)
#### Notebook Smetrics output 
 - ![image](https://user-images.githubusercontent.com/32674614/156672512-5bf0f93e-fef7-4a55-8391-7d04e20125fc.png)
#### Best model fetch in Notebook 
 - ![image](https://user-images.githubusercontent.com/32674614/156672541-43821ee1-cd28-4cf9-a8d8-6989fcef73e8.png)
 - ![image](https://user-images.githubusercontent.com/32674614/156672577-66d2a88c-0dd2-43d8-ab08-9cd41ba6ec11.png)
 - ![image](https://user-images.githubusercontent.com/32674614/156672595-9c120d38-542f-4790-b345-789895fefba2.png)
#### Notebook confusion matrix 
 - ![image](https://user-images.githubusercontent.com/32674614/156672627-04ae6565-1307-4e4c-906a-4ba5383c6b25.png)
 - ![image](https://user-images.githubusercontent.com/32674614/156672657-4f875f13-1e42-44d8-b284-254601f62877.png)
 - ![image](https://user-images.githubusercontent.com/32674614/156672678-0b83c1c8-b641-4656-86ef-d64b37e9df1e.png)
#### Pipelines 
 - ![image](https://user-images.githubusercontent.com/32674614/156672699-60b00adf-9e52-40e1-8819-a1586e6d7016.png)

#### Additional screenshots 
 - ![image](https://user-images.githubusercontent.com/32674614/156672723-7a969a1c-bbe4-4fcc-8e18-96a8b01d9658.png)
 - ![image](https://user-images.githubusercontent.com/32674614/156672753-9542a89a-e292-46ad-a6f6-655324b5232a.png)
 - ![image](https://user-images.githubusercontent.com/32674614/156672773-2cf9ade1-0840-47f0-9fec-f0544aa183e9.png)
## [Screen Recording](https://www.youtube.com/watch?v=sPJjG5x-OAg)

## Future Improvements
![image](https://user-images.githubusercontent.com/32674614/156679005-21c713c1-183c-4fd8-ab9b-887f73418193.png)
- AutoML generated Class Balancing issue , this should be considered for future improvement.
- In order to get over the above mentioned alert multiple other techniques may be used such as resampling training data, Adaptive Synthetic,Synthetic Minority Over-sampling Technique SMOTE etc.
- Model is evaluated by its accuracy to predict. However, this is not appropriate when dealing with the imbalanced dataset , prtedicting F1 , Recall , precision etc may be misleading
- SMOTE is an Oversampling technique that allows us to generate synthetic samples for minority categories and this can help to overcome Class Imbalance.
## References:
- how-to-configure-auto-train
- [how-to-configure-auto-train](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-configure-auto-train)
- how-to-configure-auto-train
- [how-to-configure-auto-train](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-configure-auto-train#configure-your-experiment-settings)
- Udacity lessons
- [Preventing overfitting](https://docs.microsoft.com/en-us/azure/machine-learning/concept-manage-ml-pitfalls)
- [data guardrails](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-configure-auto-features#supported-data-guardrails)


