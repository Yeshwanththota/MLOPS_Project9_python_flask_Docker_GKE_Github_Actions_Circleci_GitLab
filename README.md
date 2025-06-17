**Tech Stack**
<p align="left"> <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg" title="Python" alt="Python" width="40" height="40"/>&nbsp; 
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg" title="Docker" alt="Docker" width="40" height="40"/>&nbsp; 
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/kubernetes/kubernetes-plain.svg" title="Kubernetes" alt="Kubernetes" width="40" height="40"/>&nbsp; 
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/googlecloud/googlecloud-original.svg" title="GKE" alt="Google Cloud / GKE" width="40" height="40"/>&nbsp; 
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg" title="GitHub Actions" alt="GitHub" width="40" height="40"/>&nbsp; 
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/circleci/circleci-plain.svg" title="CircleCI" alt="CircleCI" width="40" height="40"/>&nbsp; 
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/gitlab/gitlab-original.svg" title="GitLab" alt="GitLab" width="40" height="40"/>&nbsp; </p>

**Highlights**
1.	CI-CD using circleci, Github Actions, GitLab

Step 1

**Project setup**
1.	Creating virtual Environment in project folder.
2.	Creating required folders and files. (artifacts for outputs, pipeline folder, src where main project code lies, (static , templates for html,css,js and flask automatically finds them in project directory), utils for common functions, requirements and setup file. To make a folder a package we need to create a __init__.py file inside it so that the methods/files can be accessed from other places.
3.	Next, we code for setup, custom exceptions, logger, requirements files (basic things at first like numpy, pandas) .
4.	Then we run setup.py in venv in cmd using pip install -e . This will install all the required dependencies for the project make the project directory ready for next steps. This step automatically created a folder with project name given in the setup.py

Step 2
1.	After jupyter notebook testing we start with Data processing.
2.	Create data_processing.py, code it and test. You should see the artifacts in the project directory.
3.	Now model_training.py in src, code it and test. Should see the model.pkl in the artifacts.
4.	Create training_pipeline.py in pipeline folder, code and run.

Step 3
**User App building using Flask**
1.	Create application.py in root , code and test. Make sure flask in requirements.
2.	Create index.html, style.css and code, Run.

Step 4

**GCP Setup**
1.	Go to Gcp and enable some API’s required for the project. 
2.	Kubernetes Engine API, google container registry API, compute Engine API, IAM API, cloud build API, Cloud storage API.
3.	Search for artifact registry. Create repo- select docker-region uscentral lowa-create.
4.	Next create a service account in IAM- name of account- permissions (owner, storage object viewer, storage object admin, artifact registry administrator, artifact registry writer)-Done.
5.	Create key for service account- hamburger- manage keys- add key- json-create.
6.	Now we need to create cluster. So go to kubernetes engine-cluster- create- give name- select region same as in GCR- tick for “access to DNS”-review-create.
Step 5
Code and Data Versioning
1.	Create Dockerfile and deployment file, code and run it.
2.	Create .gitignore
3.	Create github repo and push the code.

Step 6

**CI-CD using Github Actions**
1.	Now go to github repo settings-secrets & variables-github actions-new repo secret-give name-copy the project id from gcp and paste-create.
2.	Add another secret key- give name- copy the json content and paste in secret.
3.	Now create in root .github-workflows-deploy.yml
4.	Install github actions extension in vscode. You should a git image beside the deploy.yml
5.	Now code the deploy.yml. And push the changes to github.
6.	As configured, now the github actions triggers the CI-CD, go to actions, there you the see steps being excuted. After the successful execution, go to registry you will the image and go to GKE and workloads- you will see the pods running and endpoint. Click on it and test.

Step 7

**CI-CD using CircleCI**
1.	Add the json file to root. Rename and add to gitignore.
2.	Create .circleci folder. It automatically detects the folder. And create config.yml inside it.
3.	We write all our CI-CD code here in this file, push to github , then connect circleci and github, then github checks this config.yml file and do the deployment accordingly.
4.	Push the changes to github.
5.	Now go to circle ci on web and you can login with github or google account.
6.	I did login with github. You will see all the repos in circle ci.
7.	Select our project repo and setup triggers.
8.	 In triggers , we use ALL pushes as default. This means whatever we make changes to github, circle ci will detect and update.
9.	Now go to settings – environment variales- add the variables you mentioned in config.yml.
10.	Now for the GCLOUD_SERVICE_KEY we can’t just do it directly because when it is exposed in public, it will be automatically deactivated as said before.
11.	So go to project and open bash terminal.
12.	We need to convert the key from json to base64 format. Using $ cat key.json | base64 -w 0
13.	You will see a long code in terminal- copy it-paste it in value field in environment variable for GCLOUD_SERVICE_KEY
14.	Next add another variable GOOGLE_PROJECT_ID and give project ID from GCP.
15.	Next add GKE_CLUSTER_NAME, go to cluster name in GKE and copy-paste
16.	 Next add GKE_region, in the same page copy region-paste
17.	Now go to pipelines in circle ci- choose project if not before- click trigger pipeline
18.	Now push the changes to Github and the pipeline in circle ci should run automatically.
19.	Now you should see the run is successful in circle ci.
20.	Now to check whether the deployment is successful, go to cluster in GKE, workloads, you will see status OK and pods 2/2 running. Get inside and go the app running page.
21.	Now you can see the app running in GKE online.
22.	Done
23.	Clean up: remove artifacts repo, GKE clusters

Step 8

**CI-CD using GitLab**
1.	git remote remove origin. Because we are into GitLab now.
2.	Now create a account in gitlab and signin. Create a new project- give name- select GKE in the deployment option- make project public – untick the readme- create.
3.	Now we need to configure, go to global and run the 2 cmds in the venv.
4.	In the same page go to HTTPS.
5.	Now in terminal, git init, add branch, add remote, add, commit.
6.	Now push all the necessary code to gitLab.
7.	go to gitlab, project, settings – CI/CD-varibales-give the name for key in bottom- paste the key in value and create.
8.	Now in project root create .gitlab-ci.yml, where we write the ci-cd code.
9.	Now push the changes to gitlab.
10.	When you go to project-pipeline- you see it will be running. When you go inside you will see the steps we configured in .gitlab-ci.yml. should be green tick on all.
11.	 After some time (5-10min). go to Kubernetes cluster – workloads-you should see the OK status- go to endpoint- there your application is running-test.
12.	Done
13.	Clean up , clusters, artifacts registry etc.
