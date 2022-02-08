*NOTE:* This file is a template that you can use to create the README for your project. The *TODO* comments below will highlight the information you should be sure to include.


# Bankmarketing Data App

In this project, I am using Azure ML to perform training and find the best model using Automated ML over bankmarketing data. Then, I am deploying the best model to the endpoints, with application insights feature in it together with logging. Finally, I consume endpoints by sending data in json format to receive predictions. 

Aside from this approach, using notebook, I am creating, publishing and consuming a pipeline.

## Architectural Diagram

Dataset --> Model Training (using AutoML with particular task) --> Deployment (best model)
Logging and Applications Insights --> Consume Model Endpoints

OR

Dataset --> Model Training (or use existing experiment) --> Create Pipelines
Publish Pipelines --> Consume a Pipeline


## Key Steps

* First, data is uploaded from given URL
![Data uploaded](/screenshots/image1.png)

* Second, Auomated ML Experiment is run over this dataset with Classification task, and the best model is determined after when it is completed.
![Experiment completed](/screenshots/image2.png)

* Third, Best model is deployed, and endpoint is received, where "Applications Instights" is enabled by a logs.py script and with some logging retrieval
Here is the REST endpoint
![REST endpoint](/screenshots/image3.png)

And here is the logging retrieval
![RLogging retrieval](/screenshots/image4.png)

* After deploying the model, data posted to the endpoint and JSON output received from the endpoint as a result of deployed model. endpoint.py script also produces data.json file, which can be seen below
![JSON output](/screenshots/image5.png)

* Afterwards, as a part of the project, I run the notebook that is provided and created a pipeline
![Pipeline](/screenshots/image6.png)

* You can check the status of pipeline after its publication, which shows active in pipeline endpoint section
![Pipeline endpoint](/screenshots/image7.png)

* Here you can also check the used dataset with the AutoML module and Published pipeline overview
![Pipeline rundetails](/screenshots/image9.png)

* You can see the "Use RunDetails Widget" results in the notebook where Azure SDK is employed
![Pipeline rundetails](/screenshots/image8.png)

## Screen Recording
[Video Link](https://drive.google.com/file/d/1OC5Tz9qyelTEwHEP3oeO5x3DbDIq2ep3/view?usp=sharing)

