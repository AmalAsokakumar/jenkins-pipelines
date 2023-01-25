# A Jenkins pipeline job which integrates with AWS ECR, EC2 and EKS

This repository contains two Jenkins pipeline jobs `Jenkins` and `Jenkins-downstream` . This Jenkins job is used to build a spring boot application  

1. Job1 - To Building a Docker image form a [Spring boot application](https://github.com/comrider/springboot-app.git) and push it into AWS ECR.
2. Job2 -To Deploy the Docker image into AWS EKS.

## Prerequisites

Before using this pipeline, you will need to have the following resources available:

- Jenkins server with the following plugins installed:
  - [Parameterized Trigger](https://plugins.jenkins.io/parameterized-trigger/)
  - [Maven Integration](https://plugins.jenkins.io/maven-plugin/)
  - [Kubernetes CLI](https://plugins.jenkins.io/kubernetes-cli/)
  - [SonarQube Scanner](https://plugins.jenkins.io/sonar/)
  - [Workspace Cleanup](https://plugins.jenkins.io/ws-cleanup/)
  - [Docker](https://plugins.jenkins.io/docker-plugin/)
  - [Docker Pipeline](https://plugins.jenkins.io/docker-workflow/)



## Configuration

To use this pipeline, you will need to do the following:

1. first you need to setup two AWS EC2 instances with ubunt22.0 , t2.medium instance type 
2. install Jenkins in one instance ([to install jenkins](https://github.com/comrider/jenkins-pipelines/blob/main/installation%20notes/jenkins.MD)  )then install sonarqube ([to install sonarqube](https://github.com/comrider/jenkins-pipelines/blob/main/installation%20notes/sonarQube.md)) in the second instance.
3. push the pipeline code to git repository
4. Setup SonarQube to do continuous inspection of code quality, and Setting up  git webhook to do quality gate analysis.
5. Install and configure EKS CLI on you machine.([To create EKS cluster](https://github.com/comrider/jenkins-pipelines/blob/main/installation%20notes/installing_eks.md))
6. Setup Jenkins by install above mentioned plugins and configure the [pipeline-job-1](https://gyithub.com/comrider/jenkins-pipelines/blob/main/k8s/maven-app/Jenkinsfile),
 [pipeline-job-2](https://github.com/comrider/jenkins-pipelines/blob/main/k8s/maven-app/Jenkinsfile-downstream).  Then upload the config file form `.kube/config` as a secret text file. This file is need for providing jenkins necessary permission to deploy in EKS cluster.

## Running the Pipeline

To run the pipeline, follow these steps:

1. Push the code to GitHub repository
2. login to jenkins instance by entering `jenkins_instance_ip:8080` then we can view the progress of the job in jenkins `UI`.

## Additional Information

Jenkins pipeline is only suitable for `CI` operation because it won't provide us any information on whether the deployed application is working as expected or not. This scenario can be overcome by using tools like `Argo-CD`.