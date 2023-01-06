# Jenkins Installation

## Introduction

[Jenkins](https://jenkins.io/) is an open-source automation server that helps to automate parts of the software development process. It is a powerful tool for building and deploying applications, and it can be easily integrated with other tools in the software development ecosystem.

## Prerequisites

- [Docker](https://www.docker.com/): Required if you want to use the Docker Compose method of installation.

## Installing Jenkins

There are multiple ways to install Jenkins. Choose the method that best suits your needs.

### Method 1: Normal Installation

1. Download the Jenkins installation package from the [official Jenkins website](https://jenkins.io/download/).
2. Follow the prompts in the installation wizard to complete the installation.

### Method 2: Docker Compose

1. Install [Docker](https://www.docker.com/) and [Docker Compose](https://docs.docker.com/compose/) on your machine.
2. Create a `docker-compose.yml` file and specify the Jenkins image to use. An example `docker-compose.yml` file is shown below:

```yaml
version: '3'
services:
  jenkins:
    image: jenkins/jenkins:lts
    ports:
      - 8080:8080
      - 50000:50000
```
3. Run docker-compose up to start the Jenkins container.
Running Jenkins

4. To start the Jenkins server, run the jenkins command. You can then access the Jenkins web interface at http://localhost:8080.

## Troubleshooting

If you encounter issues with the normal installation method, try uninstalling and reinstalling Jenkins.
If you are using the Docker Compose method and the Jenkins container fails to start, try rebuilding the image with docker-compose build.

## Resources

- [Jenkins](https://jenkins.io/doc/)
- [jenkins tutorial](https://www.jenkins.io/doc/tutorials/)
