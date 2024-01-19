# AI-Planet-task


1. Setup and Configuration:
Fork and clone the FastAPI repository.
Understand the application's architecture, focusing on how FastAPI interfaces with Celery and Redis.

For the Step one i fork the repo and Clone the FastApi Repository using below commands in git bash.

git clone https://github.com/Meghamj01/fastapi-celery.git

To change the directory used below comand.

cd fastapi-celery  

To list out the files and explore used below command.

ls    

To check all the permission used below command.

ll

step 2 : Development of Deployment Pipeline:
Utilize GitHub Actions to create a Continuous Deployment (CD) pipeline.
Ensure that on merging a pull request (PR), the application is automatically deployed to a Kubernetes cluster.
You may choose any managed Kubernetes service (e.g., Google Kubernetes Engine, Amazon EKS, Azure Kubernetes Service) for deployment.



Here intially i created an instance from AWS console and 
installled git , docker in an ec2 mach8ine


then cloned a repository in ecc2 machine using 

git clone <repo_url>

cd fastapi-celery

to check all the files usind change directory command.

then i got a docker file from the repository

so i build that docker file into docker image using 

docker build -t myimage:latest <pathoffile> -f dockerfile

now i login into my docker hub account using

docker login

login into the docker hub using username and password of dockerhub account


then im going to run the image which i created using docker run command

docker run -d -p 8000:8000  <copy the tagged command>

now we created the comtainer so we have installed the k8s salso in the same container for schaling , autohealing 

mkdir k8s

docker images

so we have to create pods now so will get image from docker hub

using
docker push  megharaj685/fastapi

now to crate pod
vim pod.yaml  
Add instructions in pod file then savve it

now
docker ps
will check all the images using above command

now to create pod
will us 

kubectl apply -f pod.yaml

now pod is created 

to check we use
kubectl get pods


now we have to create deployment file
so,

vim deploy.yaml

to run the file 
kubectl apply -f deploy.yaml

to check kubectl get pods

when we delete pod its going to heal automatically its called auto healing
lets check this

kubectl delete pods fastapi

here every pod has internal ip so whenever something bad like any of the pods crashed or stop working so we come up with idea of services which will give a node port ip 
so every time we get a new pod its going to have a different ip so when we create services its not problem for us to deploy the application

so here by doing this we are done with the third step also i.e

 Implementation of Scalability:
Configure the Kubernetes deployment to enable automatic scaling. This includes scaling to zero when there's no load and scaling up from zero based on incoming traffic.
Utilize Horizontal Pod Autoscaler or any equivalent service/tool for this purpose.


now will create services 

vim service.yaml

its a node port [30000-38767]

will run services now
kubectl apply -f service.yaml

to check 
kubectl get svc

to get deployment url 

minikube service fastapi-service --url   will get url

curl -L <copied url>


now application is deployedwill goto 
vi /etc/hosts
here we are going to add ip adress of and name it

192.168.49 fastapi.com


curl -L http://fastapi.com

by using fastapi.com we are going to get the application.






