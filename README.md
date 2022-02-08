*NOTE:* This file is a template that you can use to create the README for your project. The *TODO* comments below will highlight the information you should be sure to include.


# Bankmarketing Data App

In this project, I am using Azure ML to perform training and find the best model using Automated ML over bankmarketing data. Then, I am deploying the best model to the endpoints, with application insights feature in it together with logging. Finally, I consume endpoints by sending data in json format to receive predictions. 

Aside from this approach, using notebook, I am creating, publishing and consuming a pipeline.

## Architectural Diagram




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

## Screen Recording
*TODO* Provide a link to a screen recording of the project in action. Remember that the screencast should demonstrate:

## Standout Suggestions
*TODO (Optional):* This is where you can provide information about any standout suggestions that you have attempted.
