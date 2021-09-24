OpenFaaS
===

## [What OpenFaas is?](https://www.contino.io/insights/what-is-openfaas-and-why-is-it-an-alternative-to-aws-lambda-an-interview-with-creator-alex-ellis)

OpenFaaS makes it simple to turn anything into a serverless function that runs on Linux or Windows through Docker Swarm or Kubernetes.

The target audience is developers. The idea is to make it as simple possible to create a function that is built for, deployed to and run on Docker Swarm or Kubernetes, while providing a workflow that integrates directly with the Docker ecosystem. Rather than throwing a zip file over a wall or editing in a web-form they can actually go ahead and build a Docker image from GitHub and then use the same artifact in dev, staging and production. By building on top of a container orchestration platform, you get a lot of built-in functionality such as self-healing infrastructure, auto-scaling and the ability to control every aspect of the cluster.

## [Serverless Function Made Simple](https://github.com/openfaas/faas)

OpenFaaS® makes it easy for developers to deploy event-driven functions and microservices to Kubernetes without repetitive, boiler-plate coding. Package your code or an existing binary in an OCI-compatible image to get a highly scalable endpoint with auto-scaling and metrics.

### Highlights

* Ease of use through UI portal and *one-click* install
* Write services and functions in any language with [Template Store](https://www.openfaas.com/blog/template-store/) or a Dockerfile
* Build and ship your code in an OCI-compatible/Docker image
* Portable: runs on existing hardware or public/private cloud by leveraging [Kubernetes](https://github.com/openfaas/faas-netes)
* [CLI](http://github.com/openfaas/faas-cli) available with YAML format for templating and defining functions
* Auto-scales as demand increases [including to zero](https://www.openfaas.com/blog/zero-scale/)

### Overview of OpenFaaS (Serverless Functions Made Simple)

![Conceptual architecture](images/of-layer-overview.png)

- OpenFaaS Cloud builds upon OpenFaaS to deliver GitOps with GitHub.com or GitLab self-hosted.
- NATS provides asynchronous execution and queuing.
- Prometheus provides metrics and enables auto-scaling through AlertManager.
- A container registry holds each immutable artifact that can be deployed on OpenFaaS via the API

### Conceptual workflow

![Conceptual workflow](images/of-workflow.png)

- The Gateway can be accessed through its REST API, via the CLI or through the UI. All services or functions get a default route exposed, but custom domains can also be used for each endpoint.
- Prometheus collects metrics which are available via the Gateway's API and which are used for auto-scaling.
- By changing the URL for a function from /function/NAME to /async-function/NAME an invocation can be run in a queue using NATS Streaming. You can also pass an optional callback URL.
- *faas-netes* is the most popular orchestration provider for OpenFaaS, but Docker Swarm, Hashicorp Nomad, AWS Fargate/ECS, and AWS Lambda have also been developed by the community. Providers are built with the faas-provider SDK.

**Next ->** [OpenFaaS Implementation](install.md)