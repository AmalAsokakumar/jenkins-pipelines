# Installing SonarQube on Ubuntu

SonarQube is an open-source platform for continuous inspection of code quality. It provides a central place to manage code quality, including static analysis of code to detect bugs, code smells, and security vulnerabilities.

Here is three different ways to install SonarQube on Ubuntu:

- Using the official `APT` repository
- Using` Docker`
- Building from `source
`
## Prerequisites

Before begins, make sure that we have a clean installation of Ubuntu with a `user` that has `sudo privileges` and we also need to install Java on our system. We can do this by running the following command:

```Copy code
sudo apt-get update
sudo apt-get install openjdk-8-jdk
```
### 1. Using the official APT repository

This is the recommended method for installing SonarQube on Ubuntu. It is easy and allows us to easily upgrade to newer versions when they are released.

To add the SonarQube APT repository to our system, run the following commands:
```
wget -O- https://downloads.sonarsource.com/deb/pubkey.gpg | sudo apt-key add -
echo "deb https://downloads.sonarsource.com/deb/sonarqube stable main" | sudo tee /etc/apt/sources.list.d/sonarqube.list
```

Then update the package list and install SonarQube:
```
sudo apt-get update
sudo apt-get install sonarqube
```
Once the installation is complete, SonarQube will start automatically. we can verify that it is running by visiting `http://localhost:9000` in our web browser. The default login is `admin with a password of admin`.

### 2. Using Docker

Another option for installing SonarQube is to use Docker. This is a good choice if we don't want to install SonarQube directly on our system, or if we want to quickly set up a test instance.

To install Docker on Ubuntu, follow the instructions on the [Docker](https://docs.docker.com/engine/install/ubuntu/).

Once Docker is installed, you can pull the SonarQube Docker image and run it with the following commands:

Copy code
docker pull sonarqube
docker run -d --name sonarqube -p 9000:9000 sonarqube
This will start a SonarQube container and expose it on port 9000. You can verify that it is running by visiting http://localhost:9000 in your web browser. The default login is admin with a password of admin.

3. Building from source

If you want to build SonarQube from source, you can follow these instructions:

Download the latest version of SonarQube from the official website.
Extract the downloaded archive:
Copy code
tar xzf sonarqube-*.tar.gz
Navigate to the extracted directory:
Copy code
cd sonarqube-*
Start Son