# [Open Source Serverless Cloud Platform](https://openwhisk.apache.org/)

If you want to do an implementation, please visit:

- [Local omplemtentation OpenWhisk.](install.md)

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