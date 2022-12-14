<!--
layout: page
title: "Using Variables for Helm Charts"
permalink: /https://courier-bot-coder.github.io/can.github.io/helm-variables
-->

# Using variables for Helm

This will be a demo on how to use variables to set up templates for helm charts so that you can change them easily for specific scenarios. In this example we will be using the fleetwood application that we have deployend earlier.

This content will also be found on my [github](https://github.com/courier-bot-coder/helm-variables)

For starters we can talk about how variables work with helm charts. When you create a Helm chart you will have the template folder and the values file. The template folder will hold all of the yaml files for your deployments and the values file will hold variables for those templates. within the templates you can have a path to the values file and have a basic template of a deployment and change the value in the values file for specific instances.

So for starters lets look at the original yaml file for one of the deployments on the fleet app.

```


---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: position-simulator
  namespace: default
spec:
  selector:
    matchLabels:
      app: position-simulator
  replicas: 2
  template:
    metadata:
      namespace: default
      labels:
        app: position-simulator
    spec:
      containers:
      - name: position-simulator
        image: richardchesterwood/k8s-fleetman-position-simulator:release2
        env:
        - name: SPRING_PROFILES_ACTIVE
          value: production-microservice
```
This is a standard layout for a deployment called position simulator, as demonstrated before we can deploy this and many other kinds of deployments or services using this layout. The only problem with this is that it is all hard coded directly into the yaml file. If we ever wanted something different or wanted to change a certain aspect of the application we would have to go down the list one by one of all the yaml files to change the application. Now this is where variables come in, by using variables we can create a list of variables inside the values.yaml file and create a path within the deployment files to find the wanted values. So if we wanted to make this yaml file with variables it would look like this:
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
  replicas: {{ .Values.positionSimulator.replicas }}
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
   replicas: 2
   container: 
    image: richardchesterwood/k8s-fleetman-position-simulator:release2
```

So the logic behind the pathing is that you you start from the top with the base values file and move down from there in  the values file. So when we see the top of the values file and we want to path to the image of the position simulator we start with values and then we go down with the name of position simulator and then, container, and then onto images.
The pathing should end up looking like {{ .Values.positionSimulator.container.image }}. We put the path in between 2 brackets and have periods in between all the different levels of the values file.
