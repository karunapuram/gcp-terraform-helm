# rlt_terraform_k8s
This repo holds the assets needed for the required Terraform, Kubernetes, And Helm coding

## Deployment Instructions

### Pre-Requisites

1. Download Terraform 0.12 from [here](https://www.terraform.io/downloads.html)
2. Install Docker as described [here](https://docs.docker.com/get-docker/)
3. Install Cloud SDK from [here](https://cloud.google.com/sdk/docs)
4. Install helm as described [here](https://helm.sh/docs/intro/install/)
5. Install kubctl using `gcloud components install kubectl`
6. Prepare your GCP account
	- If you do not have an account, create it
	- Make sure it is configured with payment information
	- Create a project named `rlt-test`
	- Enable The Kubernetes Engine API for this project
	- Create a service account for the project, and create an account key for it
	- Save the key in the project directory as account.json
	- Give your service account the following IAM roles:
		- Kubernetes Engine Admin
		- Service Account User permissions
		- Compute Admin
		- Storage Admin
7. Configure docker to use gcloud as a credential helper using `gcloud auth configure-docker`
8. Log in to google cloud using `gcloud auth login`
9. Configure the project value in gcloud using `gcloud config set project rlt-test`
10. Get the cluster credentials usind `gcloud container clusters get-credentials rlt-test-gke-cluster --zone us-central1`

### Deploy

1. Build the infrastructure using `terraform apply`
2. Navigate to `application/rlt-test` and build the docker container using `docker build -t us.gcr.io/rlt-test/rlt-test .`
3. Upload the container to GCR using `docker push us.gcr.io/rlt-test/rlt-test`
4. Deploy the helm chart from the root of the repository using `helm install rlt-test charts/rlt-test/`

### Use
You can access the resource using the external ip found by issuing the command `kubectl get service rlt-test`

## Overview
The purpose of this repo is to demonstrate a sample highlighting the following areas: 
* GCP
* Terraform
* Kubernetes (GKE)
* Helm

This repo holds the application code and Dockerfile in the "application" directory. The helm chart to be used to deploy the application to the Kubernetes cluster is the "charts" directory. 

## Executions
1) [x] Created Terraform code to deploy a Kubernetes cluster inside of GCP. 
2) [x] Built rlt-test application image and pushed to GCR
3) [x] Deployed the helm chart included in the repo into the kubernetes cluster.  
4) [x] Fix any issues that may be present in the helm chart.
5) [x] Exposes the application to the outside world.  

