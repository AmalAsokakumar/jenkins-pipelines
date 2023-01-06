# Installing Nexus on AWS EC2 using Docker

## Prerequisites

- An AWS account
- An EC2 instance running Ubuntu 18.04 with Docker installed
- A domain name and DNS records configured to point to the EC2 instance
- A valid SSL certificate for the domain name (optional but recommended)
## Step 1: Create a Docker Compose file

Create a file named `docker-compose.yml` with the following content, replacing `YOUR_DOMAIN_NAME` with your `actual domain name:`

```
version: '3'
services:
  nexus:
    image: sonatype/nexus3
    environment:
      - NEXUS_CONTEXT=/"
    ports:
      - "8081:8081"
    volumes:
      - ./nexus-data:/nexus-data
      - ./ssl:/ssl
    restart: always
```

## Step 2: Create a Docker network

Run the following command to create a Docker network for Nexus:

```
docker network create nexus-network
```

## Step 3: Start the Nexus container

Run the following command to start the Nexus container:

```
docker-compose up -d
```

## Step 4: Configure SSL (optional)

To enable SSL for Nexus, follow these steps:

1. Copy your `SSL certificate` and `private key` to the ssl directory on the `EC2 instance`.
2. Create a configuration file for SSL: `sudo nano /etc/nginx/sites-available/nexus.conf`
3. Add the following content to the configuration file, replacing `YOUR_DOMAIN_NAME` with your `actual domain name` and `YOUR_CERTIFICATE_AND_KEY_FILENAMES` with the names of your `certificate and key files`:

```
server {
    listen 80;
    server_name YOUR_DOMAIN_NAME;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name YOUR_DOMAIN_NAME;

    ssl_certificate /ssl/YOUR_CERTIFICATE_FILENAME.crt;
    ssl_certificate_key /ssl/YOUR_KEY_FILENAME.key;

    location / {
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_set_header X-Nexus-UI-No-Cache true;
        proxy_pass http://nexus:8081/;
    }
}
```
4. Save the configuration file and exit the text editor.
Create a symbolic link to the configuration file: 

```
sudo ln -s /etc/nginx/sites-available/nexus.conf /etc/nginx/sites-enabled/
```
Restart Nginx: 
```
sudo systemctl restart nginx
```
## Step 5: Access Nexus

You can now access Nexus at `https://YOUR_DOMAIN_NAME.`