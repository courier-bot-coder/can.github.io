<!--
layout: page
title: "Using Variables for Helm Charts"
permalink: /https://courier-bot-coder.github.io/can.github.io/helm-variables
-->

# Using variables for Helm

This will be a demo on how to use variables to set up templates for helm charts so that you can change them easily for specific scenarios. In this example we will be using the fleetwood application that we have deployend earlier.

This content will also be found on my [github](https://github.com/courier-bot-coder/helm-variables)

For starters we can talk about how variables work with helm charts. When you create a Helm chart you will have the template folder and the values file. The template folder will hold all of the yaml files for your deployments and the values file will hold variables for those templates. within the templates you can have a path to the values file and have a basic template of a deployment and change the value in the values file for specific instances.

for example if you clone the GitHub repo you will find the fleetman application but all of the yaml files are set up for variables. so our position simulator will look like this: 

```
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Values.positionSimulator.name }}
  namespace: default
spec:
  selector:
    matchLabels:
      app: {{ .Values.positionSimulator.name }}
  replicas: 2
  template:
    metadata:
      namespace: default
      labels:
        app: {{ .Values.positionSimulator.name }}
    spec:
      containers:
      - name: {{ .Values.positionSimulator.name }}
        image: {{ .Values.positionSimulator.container.image}}
        env:
        - name: SPRING_PROFILES_ACTIVE
          value: production-microservice
```

Here we can see that there is a path provided to the values file that helm can go and find the value they need. Now if we look at the values.yaml file we can look at the structure for the values:

```
replicaCount: 1
positionSimulator:
   name: position-simulator
   namespace: default
   container: 
    image: richardchesterwood/k8s-fleetman-position-simulator:release2
```

So the logic behind the pathing is that you you start from the top with the base values file and move down from there in  the values file. So when we see the top of the values file and we want to path to the image of the position simulator we start with values and then we go down with the name of position simulator and then, container, and then onto images.
The pathing should end up looking like {{ .Values.positionSimulator.container.image }}. We put the path in between 2 brackets and have periods in between all the different levels of the values file.