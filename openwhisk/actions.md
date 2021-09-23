# Install OpenWhisk - Runtime Python

# Building Python Runtime using OpenWhisk Actions

## Pre-requisites

- Gradle (recommended version: Gradle 5).
  - Java (recommended version: Java 8).
- Docker (Docker version 20.10.8, build 3967b7d).
- OpenWhisk CLI wsk.

## Previous steps

1. Open terminal and go to:

```
$ cd openwhisk-runtime-python
```


## Step 1: [Install Gradle](https://gradle.org/install/)

### Install Java 8

a. Download Java 8: [Java SE 8](https://www.oracle.com/java/technologies/javase/javase8u211-later-archive-downloads.html#license-lightbox)

b. Created the directory and unzip the files:

```
sudo tar zxvf jdk-8u291-linux-x64.tar.gz -C /usr/lib/jvm/
```

c. Open profile file:

```
sudo gedit /etc/profile
```

d. Created Java variable for bash in the end of profile file:

```
# Java path
JAVA_HOME=/usr/lib/jvm/java-7-oracle
PATH=$PATH:$HOME/bin:$JAVA_HOME/bin
export JAVA_HOME
export PATH
```

After write this, close the file with Ctrl+X and save.

e. Type the following command:

```
source /etc/environment
```

f. Restart the system to upgrade profile.

g. After restart the system, check the version of java:

```
$ java -version
```

If the response is some like this:

```
java version "14.0.2" 2020-07-14
Java(TM) SE Runtime Environment (build 14.0.2+12-46)
Java HotSpot(TM) 64-Bit Server VM (build 14.0.2+12-46, mixed mode, sharing)
```

Everything is good. You can continue with the other step.


1. Download Gradle version 5.*: [v5.6.4](https://gradle.org/next-steps/?version=5.6.4&format=bin)

## Step 2: [Install Docker](https://docs.docker.com/engine/install/ubuntu/)

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

- Java SE 8 (JDK 8u11 x64). Format: [.tar.gz](https://www.oracle.com/java/technologies/javase/javase8u211-later-archive-downloads.html#license-lightbox)

## Step 4: [Install Node.js](https://www.geeksforgeeks.org/installation-of-node-js-on-linux/)

Run in the terminal:

```
sudo apt install nodejs
```

(Node.js version: v10.19.0)


## Install OpenWhisk

**Warning**: Be sure that terminal is inside `faas_so_final_project/openwhisk/openwhisk-runtime-python`.

The runtimes are built using Gradle. The file [settings.gradle](settings.gradle) lists the images that are build by default.
To build all those images, run the following command.

```
./gradlew distDocker
```

You can optionally build a specific image by modifying the Gradle command. For example:
```
./gradlew core:python3Action:distDocker
```

The build will produce Docker images such as `action-python-v3.7`
and will also tag the same image with the `whisk/` prefix. The latter
is a convenience, which if you're testing with a local OpenWhisk
stack, allows you to skip pushing the image to Docker Hub.

The image will need to be pushed to Docker Hub if you want to test it
with a hosted OpenWhisk installation.

### Using Your Image as an OpenWhisk Action

You can now use this image as an OpenWhisk action. For example, to use
the image `action-python-v3.7` as an action runtime, you would run
the following command.

```
wsk action update myAction myAction.py --docker $DOCKER_USER/action-python-v3.7
```

## Test Runtimes

There are suites of tests that are generic for all runtimes, and some that are specific to a runtime version.
To run all tests, there are two steps.

First, you need to create an OpenWhisk snapshot release. Do this from your OpenWhisk home directory.
```
./gradlew install
```

Now you can build and run the tests in this repository.
```
./gradlew tests:test
```


**Next ->** [Python AI example](../openfaas/README.md)