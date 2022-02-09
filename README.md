# Bankmarketing Data App

In this project, I am using Azure ML to perform training and find the best model using Automated ML over bankmarketing data. Then, I am deploying the best model to the endpoints, with application insights feature in it together with logging. Finally, I consume endpoints by sending data in json format to receive predictions. 

Aside from this approach, using notebook, I am creating, publishing and consuming a pipeline.

## Architectural Diagram

Whoe architecture starts with uploading of the Dataset, which URL of to the dataset is used to import it in dataset component of the Azure ML. This dataset then connected to the AutoML module, which performed automated training for different models and parameters. Once it is completed, best model appears in the experiments, which allows you to deploy it to an endpoint. After its deployment, config.json is downloaded to the project folder and logs.py file is run from the terminal to enable application insights and some logging retrieval on the terminal. To check the endpoints, ```./swagger.sh``` was run from the git bash and then service.py file was run from the terminal to get access to swagger-ui on port 8000. Finally, endpoint.py is run in the project folder, where soring_uri and key were added manually and model prediction is received on the terminal by posting data to endpoint.

THEN

A notebook is uploaded to notebooks section directly. In the notebook, necessary libraries and functions are imported to be able to use Azure SDK. config.json again uploaded to the same directory where notebook exists, which is required to get access to workspace. Experiments and Clusters were defined, and then data is uploaded using ```Dataset.Tabular.from_delimited_files``` from given dataset URL. It is registered and converted to pandas dataframe, which follows the configuration of AutoML. After defining PipelineData for metrics and model, these two then feed into AutoML step as outputs, which all together fed to Pipeline, and then this Pipeline run. After when training is completed as AutoML experiment, pipeline is published and consumed on an endpoint

## Key Steps

* First, data is uploaded from given URL by using dataset component in Azure ML portal. This allows you to see preview of the data, their types, distributions, etc like performing an initial EDA on the dataset
![Data uploaded](/screenshots/image1.png)

* Second, Automated ML Experiment is created by selectring compute instance or cluster (I selected cluster) and run over this dataset with Classification task and metrics as AUC weighted. However, exit criterion are also determined as by determining maximum hours, which I set 1 hr, and the Concurrent was set as 5 (this number should be less then the number of the compute clusters). Then best model is determined based on their predetermined metrics score after when it is completed.
![Experiment completed](/screenshots/image2.png)

* Third, Best model is deployed as a Web Service, which Azure Container Instance is selected as deployment option and "Authentication" is enabled before confirming the deployment. However, "Application Insights" is disabled at first. Python script in the project folder is then executed to enable it. While it is enabling the Application Insights, terminal showed some retrieved logging. 
Here is the REST endpoint
![REST endpoint](/screenshots/image3.png)

And here is the logging retrieval
![RLogging retrieval](/screenshots/image4.png)

* To be able to get access to Swagger-ui, first swagger.json file downloaded from deployed model endpoint section in Azure ML portal under the name of Swagger URL, to swagger folder in the project. Then bash command ```./swagger.sh``` run to download and initialize docker image of swagger-ui on port 9000. When it is done, service.py run on port 8000. Finally, we can get access to Swagger-ui as shown below.
![swagger](/screenshots/image10.png)

* After deploying the model, and checking the endpoints with swagger, endpoint.py python script executed to receive model output on a given deployed model endpoint. It posts data to endpoint in JSON format, and terminal prints the resulting model output from the endpoint as shown below. This script also create data.json for the output, which can be found the project folder.
![JSON output](/screenshots/image5.png)

* Afterwards, as a part of the project, a notebook is uploaded to notebooks module in Azure ML portal to use Azure SDK. For notebook to identify workspace, config.json is downloaded. After defining experiment and compute clusters, data is uploaded and registered using dataset URL. Then PipelineData defined for metrics and model outputs, which are fed into the AutoML step together with AutoML config, and finally all fed into the Pipeline. This pipeline then run until AutoML completed.
![Pipeline](/screenshots/image6.png)

* When the pipeline completed, it is published by selecting the corresponding pipeline and then clicking on Publish. You can check the status of pipeline after its publication, which shows active in pipeline endpoint section. You can see details about published pipeline below.
![Pipeline endpoint](/screenshots/image7.png)

* Here you can also check the used dataset with the AutoML module and Published pipeline overview
![Pipeline rundetails](/screenshots/image9.png)

* You can see the "Use RunDetails Widget" results in the notebook where Azure SDK is employed
![Pipeline rundetails](/screenshots/image8.png)

## Screen Recording
[Video Link](https://drive.google.com/file/d/1OC5Tz9qyelTEwHEP3oeO5x3DbDIq2ep3/view?usp=sharing)

# Written description of the screencast

Here you can see the Azure ML portal homepage. It shows the recent runs, models, compute, datasets. In the run sections, we can see that there are a couple of experiments run and completed successfully. These experiments also show the type, which are Pipeline or AutoML in this case.

When we click on Models section, it shows the models list and by clicking on the particular model with particular experiment, we can reach to details about the model. By clicking on endpoints we can see the deployed endpoints. When we click on the deployed endpoints, we can reach to details about deployment status, REST endpoint, Swagger URI, etc.

If we click on Pipelines sections, we can list the pipelines that run, and from there, if we click on the pipeline endpoints, we can then list the published pipelines and their run and deployment status, which are finished and active in this case.

By clicking on the experiments, we can list the latest runs, which are Pipeline and AutoML as we demonstrated already. By clicking on the AutoML, we can get access to Pipeline and AutoML experiment list. Then, if we click on one of them, like AutoML one, we can see the details about the best model determined, and summary related to this process. IT also shows the deployment status, which is active and succeeded.

Finally, executing the endpoint.py script shows thhe response of endpoint by posting a data in JSON format to endpoint, and running this scripts runs the model and prints the model predictions, as seen in the terminal.