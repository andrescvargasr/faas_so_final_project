# Install OpenWhisk

## Prerequisites

These ports must be available:

- ```80```, ```443```, ```9000```, ```9001```, and ```9090``` for the API Gateway.
- ```6379``` for Redis
- ```2181``` for Zookeper
- ```5984``` for CouchDB
- ```8085```, ```9333``` for OpenWhisk's Invoker
- ```8888```, ```9222``` fot OpenWhisk's Controller
- ```9092``` for Kafka
- ```8001``` for Kafka Topics UI

## Step 1: [Install Docker](https://docs.docker.com/engine/install/ubuntu/)

### Set up repository

1. Update ```apt``` package index and install packages to allow ```apt``` to use repository over HTTPS:

```bash
$ sudo apt-get update
```

```
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

2. Add Docker's official GPG key:

```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

3. Use the following command to set up the *stable" repository:

```
$ echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Install Docker Engine

1. Update the apt package index, and install the latest version of Docker Engine and containerd, or go to the next step to install a specific version:

```
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

2. Verify that Docker Engine is installed correctly by running the ```hello-world``` image:

```
$ sudo docker run hello-world
```

**(Docker version: Docker version 20.10.8, build 3967b7d)**

## Step 2: [Install Docker Compose](https://docs.docker.com/compose/install/)

1. Run this command to download the current stable release of Docker Compose:

```
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

2. Apply executable permissions to the binary:

```
$ sudo chmod +x /usr/local/bin/docker-compose
```

3. Test the installation 

```
$ docker-compose --version
```

**(Docker Compose version: docker-compose version 1.29.2, build 5becea4c)**

## Step 3: [Install Java](https://www.oracle.com/java/technologies/downloads/)

Select the correct file to install in your operative system (In this case:

- Java SE 17 SDK x64. Format: [.deb](https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.tar.gz)

## Step 4: [Install Node.js](https://www.geeksforgeeks.org/installation-of-node-js-on-linux/)

Run in the terminal:

```
sudo apt install nodejs
```

(Node.js version: v10.19.0)

