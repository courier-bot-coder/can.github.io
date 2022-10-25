<!--
layout: page
title: "Vagrant"
permalink: /(https://courier-bot-coder.github.io/can.github.io/vagrant)
-->


# Creating 3 virtual machines that will have kubernetes installed and all connect together for a cluster using Vagrant

This repo will have a vagrant file and some shell files that will create 3 different virtual machines that will all connect to each other through kubernetes. you can clone this Repo using this git clone command: 
```
git clone https://github.com/courier-bot-coder/vagrant2.0.git
```
cloning this repo will get you all the important files you need to run this.

To get this running you must have virtualbox installed and also need vagrant installed. you can install vagrant by going to the official vagrant hashicorp site: https://www.vagrantup.com/downloads
 
 once vagrant is installed you can clone this repo and use this command: 
 ```
 vagrant up
 ```
 this will launch the vagrant software and connect with virtualbox to creat 3 different vms.

to destroy these vms use the command: 
```
vagrant destroy
```
