<!--
layout: page
title: "Deploying a kubernetes cluster on Azure using Terraform"
permalink: /https://courier-bot-coder.github.io/can.github.io/azure-terraform
-->

# Using Terraform to deploy a kubernetes cluster on azure
   
   This is a demo of using terraform to deploy a kubernetes cluster onto azure. All of the code can be found at [this GitHub repo](https://github.com/courier-bot-coder/terraform-template)
   
We will go ahead and begin with some prerequisite downloads.

Make sure you have the azure cli installed, you can install it on windows by using this command: 
```
choco install azure-cli
```
Once it is installed login onto your azure account using this command:
```
az login
```
now you can clone this repo by using the git clone command:
```
git clone https://github.com/courier-bot-coder/terraform-template.git
```
make sure you cd into the terraform directory. Once this is done you will need to create an Azure Active Directory Service Priniciple Account.
this is done with a simple command:
```
az ad sp create-for-rbac --skip-assignment
```
You should get an output like this :
```
{
  "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
  
  "displayName": "azure-cli-2019-04-11-00-46-05",
  
  "name": "http://azure-cli-2019-04-11-00-46-05",
  
  "password": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
  
  "tenant": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa"
}
```

From here you will want to update the terraform.tfvars file and put the appId output and the password output in between the quotes

> terraform.tfvars
```
appId    = "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa"

password = "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa"
```

now we can initiate the terraform workplace with this command: 
```
terraform init
```
Once that is done we can run this command: 
```
terraform apply
```

it will ask for verification and you will need to type out "yes"

This will apply the files and create a kubernetes cluster on azure.

From here we can access your azure portal and go to the kubernetes service tab and see our new cluster. We can now connect to that using the portal commands and deploy things from the command line.

to destroy this cluster you can use this command: 
```
terraform destroy
```
this will also ask you for a prompt and you need to type in "yes"
