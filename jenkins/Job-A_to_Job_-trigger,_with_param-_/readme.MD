# Jenkins Pipeline Job A & B

This repository contains a Jenkins pipeline job-A that can be used to trigger another pipeline job-B and also passing an parameter form job-A to job-B.

## Prerequisites

Before using this pipeline, you will need to have the following resources available:

- Jenkins server with the following plugins installed:
  - [Parameterized Trigger](https://plugins.jenkins.io/parameterized-trigger/)


## Configuration

To use this pipeline, you will need to do the following:

1. install `Parameterized Trigger` plugin from manage plugin 


## Running the Pipeline

To run the pipeline, follow these steps:

1. first create two new pipeline job-A & job-b in the `UI` 
2. Set the environmental variable in the pipeline `job-A` to trigger pipeline `job-b`

## Additional Information

This is a simple pipeline example job that i created to test out this scenario where i need to trigger a pipeline form another pipeline job.