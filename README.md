
This is a blog of all the different processes and procedures that I have learned over the course of the past year. I will list all of the different procedures that I have learned :)

Using Terraform to deploy a kubernetes cluster on azure
   
   All of these processes will be held in repos on my git hub. this repo will be found at https://github.com/courier-bot-coder/terraform-template
   
   This is a repo that breaks down the process of creating a kubernetes cluster on azure.
   
Using helm to deploy an application on a kubernetes cluster

Now that we have a kubernetes cluster up we can deploy an application using Helm. you can clone a repo for this using the git clone command again: git clone https://github.com/courier-bot-coder/fleet-web-app.git

This will break down how to get the application running on our aks cluster

Deplying a Apache Kafka cluster on kubernetes using Strimzi:

A very brief Demo on getting a Kafka cluster working, this is the very basics.

Starting off with the kubernetes cluster we will get a new namespace using this command: kubectl create namespace kafka

Now we will install Strimzi as a kubernetes cluster operator using this command: kubectl create -f 'https://strimzi.io/install/latest?namespace=kafka' -n kafka

The -n tag is designating where we want this operator. In this case its the one we just made.

Now we will want to get the Apache Kafka cluster going using this command: kubectl apply -f https://strimzi.io/examples/latest/kafka/kafka-persistent-single.yaml -n kafka 

we can use this command to wait and make sure the cluster is going: kubectl wait kafka/my-cluster --for=condition=Ready --timeout=300s -n kafka 

Once its up and running we can create a producer and consumer to send and recieve messages. To create the producer we will use this command:

kubectl -n kafka run kafka-producer -ti --image=quay.io/strimzi/kafka:0.31.1-kafka-3.2.3 --rm=true --restart=Never -- bin/kafka-console-producer.sh --bootstrap-server my-cluster-kafka-bootstrap:9092 --topic my-topic

This will create a command line prompt where we can type some messages inside it.

From here we will create a new terminal and create the consumer using this command:

kubectl -n kafka run kafka-consumer -ti --image=quay.io/strimzi/kafka:0.31.1-kafka-3.2.3 --rm=true --restart=Never -- bin/kafka-console-consumer.sh --bootstrap-server my-cluster-kafka-bootstrap:9092 --topic my-topic --from-beginning

Here we will see all of the messages that you type in the producers terminal.

This shows the bare bone ideas with kafka which allows the collection of information or content triggered by events.
