# Building a CI/CD Pipeline
## Overview
This project involves building a Github repository from scratch and creating a scaffolding that will be used to perform both Continuous Integration and Continuous Delivery for a Python-based machine learning application using the Flask web framework. It requires the use of Github Actions along with a Makefile, requirements.txt and application code to perform an initial lint, test, and install cycle. Further, the project is integrated with Azure Pipelines to enable Continuous Delivery to Azure App Service.

[![Python application test with Github Actions](https://github.com/Ezecc/project-2/actions/workflows/main.yml/badge.svg)](https://github.com/Ezecc/project-2/actions/workflows/main.yml)

## Project Plan
Below  are the links to Trello board and spreadsheet for the project.
- [Project Trello Board](https://trello.com/invite/b/IUBDY9Sp/fd665e6444e3d352039da972fe9bbead/project-2ci-cd-pipeline)

- [Initial project spreadsheet](https://docs.google.com/spreadsheets/d/1xqKjiT4MKB6uVOlxOQu0apmq0jOis8eYk-xK6Vg5MwY/edit?usp=sharing)

- [Final Project Spreadsheet](https://docs.google.com/spreadsheets/d/1-Hxu01ULV00NyDzv8BaUDq6MxsHrYBUAaKTyO5BVbls/edit?usp=sharing)


## Instructions

### Project Architecture
Below is the architectural diag the project.

![](project-2_screen_captures/Project-2_Architecture.png)
### Creating the project repository
Setup the project repository on Github with the initial project scaffold: 
- Makefile
- Tests
- code
- requirements.txt

### Creating Azure Cloud Development Environment
- Launch an Azure Cloud Development Shell Development Environment
- create ssh-keys
- upload public ssh key to the github account hosting the project repository

### Cloning the project into Azure Cloud Shell
Below is the screenshot of the project repo cloned into the azure shell development environment.

![](project-2_screen_captures/cloning_repo_in_az_shell.png)

### Updating the project scaffold and creating Python virtual environment
- Update the project files: `Makefile`, `requirements.txt` and include the project code files
- Create a Python virtual environment as follows.
    -  ```python3 -m venv ~/.myrepo```
- Activate the virtual environment by running the fowwing command.

- ```source ~/.myrepo/bin/activate```

- Create the project sript file and test files

### Performing local code test
- Test the code by running ```make all```
- A screenshot showing passing the test is shown below:

![](project-2_screen_captures/test_passing.png)

### Configure and Test GitHub Actions
Go to the Github repo and do the following:
- Enable Github Actions in the project
- Replace ```yml``` code autogenerated by enabling Github Actions with the provided ```yml```  code 
- Verify remote tests pass in Github Actions UI
as shown below:

![](project-2_screen_captures/github_action_ppassing2.png)


### Continuous Delivery on Azure
Configure Azure Pipelines to deploy the Flask starter code to Azure App Services as follows.
- Replace scaffolding code with Flask ML code
- Run the app locally as follows:
    - activate virtual environmen by running the following code:

        - ```source ~/.myrepo/bin/activate``` followed by 
        - ```python app.py```
    - Open another cloud shell environment
        - acitvate the virtual environment and run
        - ```./make_prediction.sh```
        
        The expected output is 


![](project-2_screen_captures/local_prediction_Screenshot.png.png){ width="100%" height="100" style="display: block; margin: 0 auto" }


- Deploy the app by running
- ```az webapp up -n bostonpredictionservice```
    - here, *bostonpredictionservice* is the name of the app
- copy our the generated url: ```https://bostonpredictionservice.azurewebsites.net``` to the browser and the following message will be displayed.

![](project-2_screen_captures/Screenshot_deployed_sklearn_model_in_azure.png)

- To make remote prediction: modify the project code file ```make_predict_azure_app.sh```  with your chosen app name.
- Verify prediction by running the code ```./make_predict_azure_app.sh```
- The output message is as follows:

![](project-2_screen_captures/Screenshot_azure_remote_prediction.png)

- Get log from the deployed app by running the command
```az webapp log tail``` and it displays the following output.

![](project-2_screen_captures/Screenshot_app_log_tail.png)

- Checking performance validation with ```locust```
    - modify the host name in the ```locustfile.py``` with the url of the deployed app.
    - Ensure the key names in the json under the ```predict``` function is the same as those in ```app.py```.
- Run ```locust -f locustfile.py --headless -u 20 -r 5 -t 20s```
- The expected output is

![](project-2_screen_captures/Screenshot_locust_output.png)

### Setting up CI/CD using 
- Go to the Azure DevOps organization in the portal
- Click on ```My Azure DeOps Organizations```
- Sign in
- Create a new project and give it a name, for e.g ```ci_cd_project2```
- Make sure that ```Git``` is selected as the version control and create
- Create a new service connection under the ```Pipelines``` tab after clicking on project settings
- choose ```Create service connection``` --> ```Azure Resource Manager``` --> ```Service principal (automatic) -->  ``` --> ```subsription``` 

- Choose ```Service connection name```

- login
- Choose the same resource group where the app is deployed
- Make sure the ```ci_cd_prGrant access permission to all pipelines is checked``` and save
- Go to ```Pieplines``` and create a new pipeline
- Choose ```Github```

- Configure the pipeline as ```Python to Linux Wepp App on Azure```
- Choose MSDN Platform Supsription and continue
- Sign in to Github 
- Choose the Project Repo in Github
- Validate and configure
- Check the package version then save and run
- The output is as follows.

![](project-2_screen_captures/Screenshot_azure_pipeline.png)

### Enhancements (Future Improvement Suggestions)

Some of the ways the project can be improved in the future are:
- Ensure that all needed packages are specified in the ```requirements.txt``` file.
- Provide starter codes for deep learming frameworks such as Pytorch and TensorFlow.

### Demo 

<TODO: Add link Screencast on YouTube>




<TODO:  Instructions for running the Python project.  How could a user with no context run this project without asking you for any help.  Include screenshots with explicit steps to create that work. Be sure to at least include the following screenshots:

* Project running on Azure App Service

* Project cloned into Azure Cloud Shell

* Passing tests that are displayed after running the `make all` command from the `Makefile`

* Output of a test run

* Successful deploy of the project in Azure Pipelines.  [Note the official documentation should be referred to and double checked as you setup CI/CD](https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/python-webapp?view=azure-devops).

* Running Azure App Service from Azure Pipelines automatic deployment

* Successful prediction from deployed flask app in Azure Cloud Shell.  [Use this file as a template for the deployed prediction](https://github.com/udacity/nd082-Azure-Cloud-DevOps-Starter-Code/blob/master/C2-AgileDevelopmentwithAzure/project/starter_files/flask-sklearn/make_predict_azure_app.sh).
The output should look similar to this:

```bash
udacity@Azure:~$ ./make_predict_azure_app.sh
Port: 443
{"prediction":[20.35373177134412]}
```

* Output of streamed log files from deployed application

> 

## Enhancements

<TODO: A short description of how to improve the project in the future>

## Demo 

<TODO: Add link Screencast on YouTube>


