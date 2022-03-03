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





- Deploy the best model
- Enable logging
- Swagger Documentation
- Consume model endpoints
- Create and publish a pipeline
- Documentation
