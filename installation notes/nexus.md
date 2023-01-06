# Installing Nexus on AWS EC2

## Prerequisites

- An AWS account
- An EC2 instance running Ubuntu 18.04
- A domain name and DNS records configured to point to the EC2 instance
- A valid SSL certificate for the domain name (optional but recommended)

## Step 1: Install Java

Nexus requires Java to run. To install the latest version of OpenJDK, run the following commands:

```
sudo apt update
sudo apt install openjdk-11-jre-headless
```

## Step 2: Install Nexus

1. Download the latest version of Nexus from https://www.sonatype.com/download-oss-sonatype.
2. Extract the downloaded archive: `tar xzf nexus-X.Y.Z-unix.tar.gz`
3. Move the extracted directory to the desired installation location: `mv nexus-X.Y.Z /opt/nexus`
4. Create a configuration file for Nexus: `sudo nano /etc/default/nexus`
5. Add the following content to the configuration file, replacing YOUR_DOMAIN_NAME with your actual domain name:
```
RUN_AS_USER=root
NEXUS_HOME=/opt/nexus
NEXUS_PORT=8081
NEXUS_HOST=YOUR_DOMAIN_NAME
JAVA_OPTS="-Djava.net.preferIPv4Stack=true"
```
6. Save the configuration file and exit the text editor.
7. Create a systemd unit file for Nexus: sudo nano /etc/systemd/system/nexus.service
8. Add the following content to the unit file:

```
[Unit]
Description=Nexus service
After=syslog.target network.target

[Service]
Type=simple
ExecStart=/opt/nexus/bin/nexus start
ExecStop=/opt/nexus/bin/nexus stop
User=root
Group=root
Restart=always

[Install]
WantedBy=multi-user.target
```

9. Save the unit file and exit the text editor.
10. Enable the Nexus service to start on boot: `sudo systemctl enable nexus`
## Step 3: Configure SSL (optional)

#### To enable SSL for Nexus, follow these steps:

1. Copy your SSL certificate and private key to the EC2 instance.
2. Create a configuration file for SSL: `sudo nano /etc/nginx/sites-available/nexus.conf`
3. Add the following content to the configuration file, replacing YOUR_DOMAIN_NAME with your actual domain name and `YOUR_CERTIFICATE_AND_KEY_FILENAMES` with the names of your certificate and key files:

```
server {
    listen 80;
    server_name YOUR_DOMAIN_NAME;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name YOUR_DOMAIN_NAME;

    ssl_certificate /path/to/YOUR_CERTIFICATE_FILENAME.crt;
    ssl_certificate_key /path/
```