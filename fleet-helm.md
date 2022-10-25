<!--
layout: page
title: "Using Helm to deploy an application to a kubernetes cluster"
permalink: /https://courier-bot-coder.github.io/can.github.io/fleet-helm
-->

# Using helm to deploy an application on a kubernetes cluster

Now that we have a kubernetes cluster up we can deploy an application using Helm. All this code can be found [here.](https://github.com/courier-bot-coder/fleet-web-app.git)

This is a repo that deploys an application on a kubernetes cluster using Helm.

First we will want to get Helm installed. This can be done on windows using this command: 
```
choco install kubernetes-helm
```
Making sure that you are inside the fleet-app-helm directory you can use this simple command to deploy the application on your cluster: 
```
helm install fleet-app fleet-app-helm
```
This will deploy an application using all the files found inside the templates directory

to get rid of this application, you can use the command: 
```
helm uninstall fleet-app
```
