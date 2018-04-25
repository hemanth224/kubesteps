# kubesteps


Note: 
This is a POC and No code is involved from any organization.
Public repository with Dockerhub sample nodejs microservices
https://hub.docker.com/r/hemanth224/threads/
Git Repository :
https://github.com/hemanth224


Steps to create a service in kubernetes:
Required softwares:
Java
Git
Maven
Docker
Kubectl
Azure cli

Make sure paths are added as environment variables for all these software:
export JAVA_HOME=/opt/java/jdk1.8.0_151/
export JRE_HOME=/opt/java/jdk1.8.0._151/jre 	
export PATH=$PATH:/opt/java/jdk1.8.0_45/bin:/opt/java/jdk1.8.0_151/jre/bin:/opt/maven/apache-maven-3.2.1/bin;/opt/kubernetes

Clone the git repository in some folder e.g
Go to the folder where there is pom.xml and run mvn clean and mvn install
Build the docker using the command below:
docker build -f DockerFile -t  .
	Once done, verify that the image is created using the below command:
	docker images
Login to the docker repository 

docker login -u  -p

Push the image to docker repository
docker push to docker repository

Once pushed the image to docker container registry, there are two ways to deploy the application: 
1. Kubectl commands 2. Kubernetes dashboard
For both the ways, first step is to download the cluster configuration information. For this execute the below steps:
From command prompt, login to azure cli using your azure credentials:

az login -u hemanth -p <<password>>

Create a folder in your local machine. Inside that folder, and keep the following private key file in that folder (say that folder is /usr/local/acs).
Execute the below command

az acs kubernetes get-credentials --resource-group=
Once done, you are ready to deploy the application using kubectl or kubernetes dashboard

Using kubectl command

kubectl run  --image=hemanth224/threads

Expose your Kubernetes cluster externally by using the kubectl expose command. Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on. For example:
kubectl expose deployment threads  --type=NodePort --port=80 --target-port=8080

It will take some time for deployment. Once done, you can run the below command to check the external IP exposed. Service will be available here.

kubectl get services

Now if another version of image to be deployed, run all the steps 1-5. Do increment the version in the docker image tag. Once done run the below command:
kubectl set image deployment hemanth224/threads

Using kubernetes dashboard 
kubectl proxy
Execute the below command. It will start the kubernetes dashboard on http:/127.0.0.1:8001


From there, follow the steps in https://docs.microsoft.com/en-us/java/azure/spring-framework/deploy-spring-boot-java-app-on-kubernetes to deploy from UI.

