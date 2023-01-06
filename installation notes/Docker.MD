# Docker Installation

## Introduction

[Docker](https://www.docker.com/) is a containerization platform that allows you to package and deploy applications in lightweight, isolated containers. It is a powerful tool for developing, testing, and deploying applications quickly and consistently.

## Prerequisites

- [Supported operating system](https://docs.docker.com/engine/install/#supported-platforms): Docker is supported on a variety of platforms, including Windows, macOS, and Linux. 

## Installing Docker

There are multiple ways to install Docker. Choose the method that best suits our needs.

### Method 1: Normal Installation

1. Download the Docker installation package from the [official Docker website](https://www.docker.com/products/docker-desktop).
2. Follow the prompts in the installation wizard to complete the installation.

### Method 2: Using a Package Manager

1. Install the package manager on our machine (e.g., `apt-get` for Ubuntu, `yum` for CentOS).
2. Use the package manager to install Docker. For example, on Ubuntu, run the following command:

```bash
apt-get update
apt-get install docker-ce
```
## Method 3: Building from Source

Install the necessary dependencies for building Docker from source. On Ubuntu, these dependencies can be installed with the following command:
```
apt-get update
apt-get install -y build-essential libssl-dev
```
Clone the Docker repository from [GitHub](https://github.com/docker/docker.git) `git clone https://github.com/docker/docker.git`

Build and install Docker from source:
```
cd docker
make
make install
```
## Running Docker
To start the Docker daemon, run the dockerd command. We can then use the docker command to create and run Docker containers. For example,
```
docker run ubuntu:18.04
```
This will run a container based on the ubuntu:18.04 image
 we can use the `-it` option to run the container in interactive mode and also use the `-d `option to run the container in detached mode. Use the `docker ps` command to view the list of running containers, and the `docker stop` command to stop a running container.