Function as a Service - FaaS
===

Final Project
---

## Operative Systems and Network Services
### Semester I, 2021
### Universidad del Valle
![Logo Univalle](logo_UV.gif)



# Introduction

This reposirory contain a brief description about FaaS and show a comparison between differents platforms available. More, you can see two real implementations: OpenWhishk and OpenFaaS with Jupyter Notebook (Tensorflow example instead).

1. [Brief Introduction to FaaS](introduction/README.md)
2. [FaaS platforms comparison](faas_comparison/README.md)
3. [OpenWhisk](openwhisk/README.md)
   1. [OpenWhisk implementation](openwhisk/install.md)
      1. [Local building](openwhisk/local.md)
      2. [OpenWhisk Actions](openwhisk/actions.md)
         1. [Jupyter Notebook: Python AI example](openwhisk/python_AI_example.md)
4. [OpenFaaS](openfaas/README.md)
   1. [OpenFaaS implementation](openfaas/install.md)

Root tree:

- faas_comparison
  - [README.md](faas_comparison/README.md)
- introduction
  - [README.md](introduction/README.md)
- openfaas
  - [README.md](openfaas/README.md)
- openwhisk  
  - [README.md](openwhisk/README.md)
  - [install.md](openwhisk/install.md)
  - [local.md](openwhisk/local.md)
  - [actions.md](openwhisk/actions.md)


## Cloning the project

This project uses SUBMODULES.

In order to clone it use:

```
git clone --recurse-submodules https://github.com/andrescvargasr/faas_so_final_project.git
```

## Pull and update submodules

You should run this command every time you want to pull:
`git pull --recurse-submodules`

## Submodules update only

To update the submodules:
`git submodule update --recursive --remote`