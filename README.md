# faas_so_final_project

This reposirory contain a brief description about FaaS and show a comparison between differents platforms available. More, you can see two real implementations: OpenWhishk and OpenFaaS with Jupyter Notebook (Tensorflow example instead).

- Brief Introduction to FaaS: <https://github.com/andrescvargasr/faas_so_final_project>


# [Open Source Serverless Cloud Platform](https://openwhisk.apache.org/)

## What is Apache OpenWhisk?

Apache OpenWhisk is an open source, distributed Serverless platform that executes functions (fx) in response to events at any scale. OpenWhisk manages the infrastructure, servers and scaling using Docker containers so you can focus on building amazing and efficient applications.

![OpenWhisk](OW-Abstract_Architecture_Diagram.png)

The OpenWhisk platform supports a programming model in which developers write functional logic (called Actions), in any supported programming language, that can be dynamically scheduled and run in response to associated events (via Triggers) from external sources (Feeds) or from HTTP requests. The project includes a REST API-based Command Line Interface (CLI) along with other tooling to support packaging, catalog services and many popular container deployment options. 


## Deploys anywhere

Since Apache OpenWhisk builds its components using containers it easily supports many deployment options both locally and within Cloud infrastructures. Options include many of today's popular Container frameworks such as Kubernetes and OpenShift, and Compose. In general, the community endorses deployment on Kubernetes using Helm charts since it provides many easy and convenient implementations for both Devlopers and Operators alike.

## Write functions in any language

Work with what you know and love. OpenWhisk supports a growing list of your favorite languages such as Go, Java, NodeJS, .NET, PHP, Python, Ruby, Rust, Scala, Swift and even newer, cloud-native ones like Ballerina. There is even an experimental runtime for Deno in-development.

If you need languages or libraries the current "out-of-the-box" runtimes do not support, you can create and customize your own executables as Zip Actions which run on the Docker runtime by using the Docker SDK. Some examples of how to support other languages using Docker Actions include a tutorial for Rust and a completed project for Haskell.

Once you have your function written, use the wsk CLI, to target your Apache OpenWhisk instance, and run your first action in seconds. 




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

2. Add Docker's official GPGP key:

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
