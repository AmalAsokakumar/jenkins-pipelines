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

1. first you need to setup two AWS EC2 instances
2. install Jenkins in one aws EC2 instance we can name it as Jenkins instance. 

## Running the Pipeline

To run the pipeline, follow these steps:

1. [Add steps for triggering the pipeline here]
2. [Include any additional steps needed to run the pipeline]

## Additional Information

[Include any additional information or notes about the pipeline here]