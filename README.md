#Documentation of the Project 
Project 7 : Minor MLOps project - 2 Using GitLab CI-CD
In this project we will learn GitLab CI-CD, we will deploy on Google Kubernetes cluster.
Folder Name & Path : MLOps-Beginner to Advanced MLOps on GCP-CICD_ Kubernetes Jenkins/7_Project
Highlights of the Project : 
1.Use of GitLab, this will be used as source code management and CICD tool. 
2.Making Kubernetes Cluster on Google Kubernetes cluster
WorkFlow of the project: 
Here Data Ingestion part is not explained again, we can implement the same steps as mentioned in the previous projects.
1.Project setup: We define project and folder structure, custom Exception, logging, create virtual environment.  
2.Jupyter Notebook Testing: We will do notebook testing on EDA, Data processing , and all required steps. 
3.Data Preprocessing  : 
4.Model Training : 
5.User App building : We will use flask for building app. 
6.Training Pipeline : 
7.Data and Code Versioning using GitLab :  Here we will use GitLab for Source code management and CI-CD tool. 
8.GCP Setup : Here we will create Kubernetes cluster on Google cloud, artifacts repository, service account, creating keys. 
9.CI-CD Deployment using GitLab CI-CD :  We will use GitLab for deployment. We will use Docker, Google container registry(to store image in GCR), we will deploy the image from GCR to Kubernetes GKE. 
10.Done.


How GitLab is different from Github.

GitHub : 
- In github we will create Open source projects. 
- Github uses Github actions for CI-CD
- We can either go for basic security or advanced security(if paying).
- Easier to use
 - Choose Github when the project is Open source, user friendly

GitLab :  
- In Gitlab we will create private projects(real time projects).  
- GitLab has built in CI-CD
- We will get stronger security
- Easier to use.
- Use Gitlab when working for a company on the project. 

Dockerize the  project(Image) --> Push the docker image to  GCR--> GitLab -->  GKE .

How GitLab is different from jenkins.

GitLab : 
	- Setup : Integrated CI CD
	- Customizations : limited
	- Cost : Free, If its basic. Paid, if it s company project. 

Jenkins : 
	- Setup : Manual setup
	- Customizations : more options
	- Cost : free

Now Starts with Project Code Setup Implementation.
1. Project Setup Implementation : 
Create a folder for the project on Laptop. From this folder path type CMD and enter, then run code . , this will take you to VS Code. Now Go to VS Code, open terminal
Create virtual environment
-Python -m venv venv
-Another way of Creating virtual environment 
	Conda create -p venv python==3.10.0 -y
Activate virtual environment
-Venv\Scripts\activate
-Conda activate venv/
Create a setup.py file.
Now start with project structure. Create below files/folders. To make any folder as a package, create __init__.py file 
-Create requirements.txt
-Create setup.py
-Create src folder. To make this folder as a package create __init__.py file.
-Create Config folder. To store configurations.
-Create Notebook folder
-Static folder
-Templates folder  
-Artifacts folder. To store the CSV files, processed files, model.
-Pipeline folder
Now src folder should be treated as a package, that means you define some function in one file and import it in another file. For that run “pip install -e .” in terminal.
Create a folder RAW in artifacts folder and copy the data into it. 

2. Jupyter Notebook Testing :
In VS Code, Extensions install Jupyter Extension. Now Create notebook.ipynb file in Notebook folder. Create a new cell and just run, select the environment. Again run empty cell for installing the Ipykernal. 

3. Data Preprocessing :

In Src folder create a data_processing.py file. Add the required code in this file. Define init constructer, load_data, preprocess_data, feature_selection,  split_and_scale_data, save_data_and_scaler, run methods. 


4.  Model Training :
In src folder crate a model_training.py file. Create a class ModelTraining in the file. Initialise the parameters. Load_data, train_model, evaluate_model.
	
5.User App Building:
Now let’s start with User App building. Now create folders static, templates in Project directory. Now create index.html file in templates folder and style.css file in static folder. Add the required code in this files. We can gett index.html and styles.css code from chatgpt.
Create an Application.py file in project directory.  Add the required code. Then run python application.py , this will provide an URL for web app. 

6.Training Pipeline: 
Now in pipeline folder create a file training_pipeline.py. Then run python pipeline/training_pipeline.py

7.Data and Code Versioning using GitLab :
Now let’s start with Data and Code versioning. Here we will use GitLab for both data and code versioning. 
Now in .gitignore file, add all the folders which are not required, add venv, logs,  MLOps_Project_7.egg-info. We will not add Artifacts folder in .gitignore file because we want this for data versioning. 
Now go to browser , search for gitlab and create an account in Gitlab. Now in Gitlab dashboard -->Projects --> New project --> create a blank project --> Provide a name for the project ,, choose deployment target as Kubernetes,, make it public ,, uncheck the Readme file,,--> click on create project. Project is created. 
- Now login to Gitlab and create a new repository.  
	            Using gitlab account credentials , rajasekharvardhi@gmail.com, RaJuArJuN$89. 
Created MLOps-project-7 project.
Now it will ask for whether local or global setup, choose global. Copy the commands that shown as below, Now open VS Code terminal command prompt, run
	- git config --global user.name "Raja Sekhar Vardhi"
- git config --global user.email "rajasekharvardhi@gmail.com"
Now with this we have configured our Gitlab into VS Code.
Now make sure git is installed. Check git --version.
Now select HTTPS, copy the commands that shown as below and run
	-  git init , to initialize the git repository
	- git branch -M main
- git remote add origin https://gitlab.com/rajasekhar899/mlops-project-7.git
- git add .
- git commit -m “pushing code to git”
- git push --set-upstream origin main
- Code is pushed to Gitlab. Just refresh the page in Gitlab.
Data and Code versioning is done.

8.GCP and CI-CD Setup :
Important step in the project.  
Install Google cloud CLI on computer (https://cloud.google.com/sdk/docs/install)
-Once installed, to verify , close and open VS Code, and then in terminal run “gcloud – version “ 
Logged into GCP using rajasekharvardhi@gmail.com mail. Once logged in we need to enable some API’s as mentioned below ,go to API Library 
- Kubernetes Engine API 
- Google Container Registry API
- Compute Engine API
- Cloud Build
- Cloud Storage
- IAM
Creating a Kubernetes Cluster
In the Gcp console --> Kuberenetes Engine --> Clusters --> Create --> Provide a name for the cluster(my-cluster) --> In Control Panel Access, select Access using DNS, Access using IPV4 networks --> click on Create cluster.  This will take some time for creation. 
Create a Service account
Steps : 
1.Create a service account in GCP
-To create a service account,  go to IAMservice accountsProvide a name for Service account (ci-cd-deployment)-->create and continue -->  create role as Owner,, Storage object viewer,, Storage object admin ,, Artifact registry Administrator,, Artifact registry Writer. --> continue --> Done. 
Created service account 
-Then again go to service account click on 3 dots,  under Key ID , there are no keys, for that go to manage keys add key create a new key --> select Json key and download.
-Now copy the downloaded service account key into the VS Code directory. Rename it to gcp-key.json for convinience.
-Add this file(gcp-key.json) into .gitignore file, we don’t want this to push to Github.
-After making these changes push the code again to Github. 

Create Artifact Registry
Now go to Artifact Registry --> Create a Registry --> Provide a name (my-repo) , choose as Docker,, choose region,, --> Click on Create.  For now this repo is empty, we will store the project docker image here only. 
We have created this artifact registry Is for whatever the project docker image we create will be stored here. 

Now install Docker extension in VS code.
Now create a Dockerfile file in VS Code project directory.  
Now create a kubernetes-deployment.yaml file in VS Code project directory.  Create the file. In the file provide the metadata name from the artifact that is create above from Artifact Registry.
metadata:
  name: mlops-app

Provide the container port from application.py file. 
Provide the image full path from artifact repository that is create above  Artifact Registry. Note : Copy the  image path after the deployment is done. 
spec:
      containers:
        - name: mlops-app-container
          image: us-central1-docker.pkg.dev/mlops-new-447207/mlops-app/mlops-app:latest
 # project name/ image name
          ports:
            - containerPort: 5000 # Replace with the port your app listens on

we need to convert gcp-key.json file into base64 format, because we can’t make this key public. We have already copied this key into VS code project directory. So that’s why we need to convert it into base64 format. for this  in VS Code terminal , Git bash , Run as below
	-  cat gcp-key.json | base64 -w 0
	-  This will provide a encoded data, Copy the data)

Add Environment Variables

Now go to Gitlab dashboard on browser , in the repo --> settings --> CI/CD -->  variable --> add variable -->  Provide key as : GCLOUD_SA_KEY and in Value segment paste the copied encoded data from above line --> click on Add variable. 

Now comes the important part GitLab CI-CD 
	- Create a file .gitlab-ci.yml in VS Code project directory.Add the required code.
image: google/cloud-sdk:latest

stages:
  - checkout
  - build
  - deploy
variables:
  PROJECT_ID: "mlops-new-447207"  ## Project id from GCP console
  REGION: "us-central1"
  REPO: "my-repo"   ##  GCP artifact registry Repo name 
  REGISTRY: "us-central1-docker.pkg.dev" ## GCP artifact registry Repo registry name
  CLUSTER: "my-cluster"  ## GCP Kubernetes cluster name
checkout_code:
  stage: checkout
  script:
    - echo "Code Checked out.."  ## Just priniting
build_docker_image: ## Building Docker image
  stage: build
  services:
    - name: docker:dind ## In google there is no DOcker, that’s why why we are building docker
      command: ["--tls=false"] ## to prevent issues
  variables: ## Docker variables
    DOCKER_HOST: tcp://docker:2375 
    DOCKER_TLS_CERTDIR: "" ## Prevent docker demoen from using tls
  before_script:
    - echo "$GCP_SA_KEY" | base64 -d > key.json  ## Decoding GCP key variable saved in gitlab
    - gcloud auth activate-service-account --key-file=key.json ## Authenticate GCP service account
    - gcloud auth configure-docker $REGISTRY ## Authenticate docker 
  script:
    - docker build -t $REGISTRY/$PROJECT_ID/$REPO/mlops-app:latest .  ## Building the image, image name should be same as the kubernetes-deployment file image
    - docker push $REGISTRY/$PROJECT_ID/$REPO/mlops-app:latest  ## Pushing the image to docker 
deploy_to_gke:  ## Deploying to Google kubernetes, we can provide any name 
  stage: deploy
  before_script:
    - echo "$GCP_SA_KEY" | base64 -d > key.json
    - gcloud auth activate-service-account --key-file=key.json
    - gcloud auth configure-docker $REGISTRY
  script:
    - gcloud container clusters get-credentials $CLUSTER --region $REGION --project $PROJECT_ID
    - kubectl apply -f kubernetes-deployment.yaml  ## Deploying kubernetes file

We are done with creation of code.
Now we push the code to Gitlab. As soon as we push the code to Gitlab , pipelien automatically get triggers. We can check this in Gitlab dashboard --> Build --> Pipelines. 

Now with this we have deployed our Project. Now wait for 2-3 minutes. 
Now go to Gcp Kubernetes Engine console , we can see the cluster status as success . Go to Workloads --> click on the available workload --> Here if you come to end , we can see Endpoint where the app is running. 

With this we have succesfully deployed our application in Google Kubernetes Engine through GitLab CI-CD. 

9.Done

