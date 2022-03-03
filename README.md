# Operationalizing Machine Learning
## Overview
In this project, you will continue to work with the Bank Marketing dataset. We will use Azure to configure a cloud-based machine learning production model, deploy it, and consume it. W will also create, publish, and consume a pipeline. 

## Project main steps
In this project, you will following the below steps:

- Authentication
I have usedthe lab Udacity provided and thus I have skipped this step since I am  not authorized to create a security principal. 

- Automated ML Experiment
 In this step, I have created an experiment using Automated ML, configure a compute cluster, and use that cluster to run the experiment.
 
  - ### Dataset used
  - [bankmarketing_train](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv)
  - ### Steps For Creating Dataset in MLOps
  - 1.
  ![image](https://user-images.githubusercontent.com/32674614/156611711-ba85d269-409e-43df-8b26-87ce068de757.png)
` - 2.
 ![image](https://user-images.githubusercontent.com/32674614/156611814-f70a0e94-38a6-4f08-ae57-3ecd96c3dfda.png)
 - 3.
 ![image](https://user-images.githubusercontent.com/32674614/156611944-734510d2-9300-4284-9914-6d9ff3c1883b.png)
 - 4.
 ![image](https://user-images.githubusercontent.com/32674614/156612041-c468f206-e973-4f27-abca-20d8b97e6fd2.png)
 ![image](https://user-images.githubusercontent.com/32674614/156612108-164d9a3a-8234-4f5a-b006-cfedd913cba6.png)
 ![image](https://user-images.githubusercontent.com/32674614/156612162-89f2888b-0433-4718-a195-4addf2b75e0e.png)
 - 5.
 ![image](https://user-images.githubusercontent.com/32674614/156612243-f391ce6d-08af-4f31-9d19-3d147faca0a2.png)

- ### Creation of Compute Cluster
   - ![ComputeCluster](https://user-images.githubusercontent.com/32674614/156613032-8d31be24-feb6-4354-98b3-bcb30471b70d.png)
- ### Creation of Compute Instance
  - ![ComputeInstance](https://user-images.githubusercontent.com/32674614/156613199-b6091322-bac0-4524-b7bf-a038631d3583.png)
- ### Creating a New Automated ML run
  - 1. 
  - ![image](https://user-images.githubusercontent.com/32674614/156613542-76096ec1-d872-45e4-9c12-2ed691d39c60.png)
  - Selecting Classification
  - ![image](https://user-images.githubusercontent.com/32674614/156613617-07729628-c185-41f1-9625-99222e45fd28.png)
  - ![image](https://user-images.githubusercontent.com/32674614/156613667-9fed6a73-dad3-4a55-bb77-cd1131936d00.png)
  - ![image](https://user-images.githubusercontent.com/32674614/156613712-d709b690-06ef-47ce-8aba-be0e993a8ed3.png)
  - ![image](https://user-images.githubusercontent.com/32674614/156613761-8108eec8-cb6d-48dc-90c5-bcdef7f83f0b.png)
- ### Screenshot of Experiment complete
  - ![image](https://user-images.githubusercontent.com/32674614/156613926-af70145d-02ba-4c86-a500-0bc6e5e4a1ed.png)
- ### Screenshot of best model
  - ![image](https://user-images.githubusercontent.com/32674614/156614087-18a06e4c-1d2c-463c-881a-0905ee8f9768.png)
- ### metrics of best model VotingEnsemble
  - ![image](https://user-images.githubusercontent.com/32674614/156614333-31292657-c0b8-421d-bc86-d0deba3cde91.png)
  - ![image](https://user-images.githubusercontent.com/32674614/156614492-f2d89e6d-269c-47b2-bb01-d9cfda0b4948.png)
  - ![image](https://user-images.githubusercontent.com/32674614/156614526-349fde6c-f4d3-4f72-bf18-33f785e72cc1.png)
  - ![image](https://user-images.githubusercontent.com/32674614/156614566-83425c57-dd7b-4968-8850-1c4143263e51.png)
  - ![image](https://user-images.githubusercontent.com/32674614/156614610-7cb1e459-ba22-41df-b230-71a0ccd397cc.png)
  - ![image](https://user-images.githubusercontent.com/32674614/156614654-5944aa8d-bbb9-4688-a890-0cca20e282cb.png)
  - ![image](https://user-images.githubusercontent.com/32674614/156614690-9ba4b6a7-44ad-4ac8-a43b-f7d52cc2a300.png)
- Deploy the best model
   #### Deploying the Best Model will allow to interact with the HTTP API service and interact with the model by sending data over POST requests.(enable Application Insights )
  - ![image](https://user-images.githubusercontent.com/32674614/156615159-8e43c573-ebc3-4198-ba57-71da0ed07e9a.png)
  - ![image](https://user-images.githubusercontent.com/32674614/156615213-4d7e4252-da56-42e5-8d32-4d07f145552e.png)
  - ![image](https://user-images.githubusercontent.com/32674614/156615271-b2a02358-ee8f-4d44-8949-d727e0c2fc35.png)
  - ![image](https://user-images.githubusercontent.com/32674614/156615547-106bbe1a-9dfb-45c1-bc1e-53d3b053ef46.png)
  - ![image](https://user-images.githubusercontent.com/32674614/156615604-7691bd5f-7747-4693-96ab-d6fa7bde0a60.png)
  - ![image](https://user-images.githubusercontent.com/32674614/156615644-0c0a633b-2199-4325-8c73-d99cb92d8473.png)

- Enable logging
  ## Step 4: Enable Application Insights
     Now that the Best Model is deployed, enable Application Insights and retrieve logs. Although this is configurable at deploy time with a check-box, it is useful to be able   to run code that will enable it for you.
     - Add following code to logs.py
```
     name = "automlvotingensemble"
     service = Webservice(name=name, workspace=ws)
     service.update(enable_app_insights=True)
```
     
- Swagger Documentation
- Consume model endpoints
- Create and publish a pipeline
- Documentation
