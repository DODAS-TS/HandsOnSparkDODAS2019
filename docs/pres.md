# Hand-on session

# DODAS generated Spark cluster

### Contact: diego.ciangottini<at\>pg.infn.it

---

# Overview

- Objective recap
    - Deploy your own cluster
- Templating applications with Helm
    - Simple function example
- User interfaces for Spark on Dodas
    - Experimenting base features
    - Debugging

---

# K8s on DODAS

<img src="img/k8s-dodas.png" width=600>

---

# Spark on DODAS

<img src="img/k8s_spark_cut.png" width=800>

---

# Setup architecture: recap

- __1 Master pod__:
    - __Spark driver__
    - __Jupyter__

- __Services__:
    - __Jupyter__
    - __Spark webUI__
    - __K8s dashboard__

- __At notebook python Kernel start__:
    - __2 executor pods__

Directly from the notebook is also possible to stop the current spark context and to reload a new one with different executors.

---

# Setting up you environment

## Download the Hands-on repo

    !bash
    wget https://github.com/DODAS-TS/HandsOnSparkDODAS2019.git
    cd HandsOnSparkDODAS2019

## Copy your DODAS configuration template

    !bash
    cp templates/dodas_template.yaml ~/.dodas.yaml

### Quick look at DODAS client configuration

    !yaml
    cloud:
        id: ost
        type: OpenStack
        host: https://horizon.cloud.cnaf.infn.it:5000/v3
        username: iam-demo 
        password: token_template 
        tenant: oidc 
        auth_version: 3.x_oidc_access_token
        service_region: regionOne
        auth_url: "https://horizon.cloud.cnaf.infn.it:5000" 
    im:
        id: im
        type: InfrastructureManager
        host: https://im-demo.cloud.cnaf.infn.it/infrastructures
        token: token_template 

## Retrieve you access token from IAM

### Import the pre-configured client for the demo
 
    !bash
    export IAM_DEVICE_CODE_CLIENT_ID=7b50c794-c45a-45ad-906f-83cb18e36a5d

    export IAM_DEVICE_CODE_CLIENT_SECRET=AJTXpc_Mo4ZgtcO7cT5CYYFHEQbeaV5IVYTiU4YQFoHyDMYZWiDPqvgmWLSV6ryBfF-HVbzLujPpgemifvVWcTY

### Retrieve the token

Simply run and follow the instructions:

    !bash
    ./scripts/get_token.sh

### Check $HOME/.dodas.yaml file correctly filled

---

# Install DODAS client

## Documentation

You can find a quick start guide and reference guide [here](https://cloud-pg.github.io/dodas-go-client/)

## Download the binary

    !bash
    wget https://github.com/Cloud-PG/dodas-go-client/releases/download/v0.3.0-rc2/dodas.zip
    unzip dodas.zip

## Test the installation



---

# Deploy your cluster

## Get TOSCA template

    !bash
    less templates/spark_template.yml

## Understand the configuration parameters

## Deploy the cluster

## Check the status

---

# Helm: introduction exercise

## What's Helm

## Install Helm

## Simple example

### Init your chart

---

# Helm: "chart up" your application

## Application 1

## Application 2

## Test your Helm chart

## Publish the chart

Reference [documentation]()

---

# Spark HELM chart

## Values 

As you can see following the link in the TOSCA template. The values needed for the deployment are:

    !yaml
    Spark:
        Path: /opt/spark

    externalIP:
        enabled: true
        ip: {{ externalIP }}

    Master:
        Name: master
        Image: cloudpg/spark-py
        ImageTag: dodas-2.4.3-bigdl
        Replicas: 1
        Component: spark-master
        Cpu: 100m
        Memory: 1024Mi
        ServicePort: 7077
        ContainerPort: 7077
        # Set Master JVM memory. Default 1g
        # DaemonMemory: 1g
        ServiceType: ClusterIP
    Jupyter:
        NodePort: 30888

---
# Time to play with Spark cluster

## Debugging

### Kubernetes Web-UI

### Spark Web-UI

### Log into the k8s master

--- 

# Using Jupyter

## Load the exercise notebook

### Check the executor pods appearing 

## Basic functional test

### Calculate Pi

    !python
    def test:

---

# Spark playground


---
