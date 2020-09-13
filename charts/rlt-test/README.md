Pre Requisites for Helm : 

You have basic knowledge of how to build Docker images.
You have basic knowledge of Helm charts and how to create them.
You have a Docker environment running.
You have an account in a container registry 
You have a Kubernetes cluster running.
You have the kubectl command line (kubectl CLI) installed.
You have Helm v3.x installed.

Steps for install helm chart into kubernetes cluster : 


Step 1: Obtain the application source code


Step 2: Build the Docker image

docker build -t us.gcr.io/rlt-test-289320/rlt-test .
gcloud auth configure-docker
docker tag rl-test us.gcr.io/rlt-test-289320/rlt-test

Step 3: Publish the Docker image

docker login
docker push us.gcr.io/rlt-test-289320/rlt-test

Step 4: Create the Helm Chart

Helm Chart is already provided in the repo but we need to edit in value.yaml.

values.yaml: This file declares variables to be passed into the templates. It is important to replace the USERNAME with your Docker ID, and also to check if the container name and version exist.

image: 
repository: us.gcr.io/rlt-test-289320/rlt-test
tag: 0.1.0

Step 5: Deploy the example application in Kubernetes

First, make sure that you are able to connect to your Kubernetes cluster by executing the command below:
kubectl cluster-info

helm install rlf-test

Run the kubectl get pods command to get a list of running pods:
kubectl get pods