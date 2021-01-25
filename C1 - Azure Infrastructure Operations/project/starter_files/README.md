# Azure Infrastructure Operations Project: Deploying a scalable IaaS web server in Azure

### Introduction

This is the first project of the Azure DevOps nanodegree, where students must deploy a web server in Azure using terraform and packer.

### First Steps
1. Firstly, we need an [Azure Account](https://portal.azure.com) 
2. After getting an Azure account, we must install the [Azure command-line interface](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
3. To create and deploy the Virtual Machine (VM) image, we need [Packer](https://www.packer.io/downloads)
4. For automated creation of our infrastructure, we need to install [Terraform](https://www.terraform.io/downloads.html)

### Policy Deployment

Before deploying the infrastructure needed for this project, we must create a policy that ensures all indexed resources are tagged. This policy will help us with organization and tracking, making it easier to log when things go wrong. For this task, we should use the Azure Policy tool found inside the security center. According to the given specifications, the policy to be created should **deny** the creation of resources that **do not have tags**.  

There are many ways to accomplish this task, such as using the Azure Portal, Azure Command Line (CLI), or using Terraform. I chose the latter to make it scriptable. The policy is depicted below.

~~~
{
    "type": "Microsoft.Authorization/policyDefinitions",
    "name": "deny-creation-resources-without-tags", 
    "properties": {
        "mode": "all",
        "displayName": "tagging-policy",
        "description": "Deny the creation of resources that do not have tags in Azure.",
        "policyRule": {
            "if": {
                "allof": [
                    {
                        "field":  "tag",
                        "exists": "false"
                    }
                ]
            },
            "then": {
                "effect": "deny"
            }
        }
    }
}
~~~

### Packer Template

In order to support application deployment, we need to create an image that different organizations can take advantage of to deploy their own apps.To do this, we need to create a packer image that anyone can use, and we will leverage in our own Terraform template. To do so, we use packer to create a server image, ensuring that the provided application is included in the template. In order to complete the requiments of this project, the template ....

* Use an Ubuntu 18.04-LTS SKY as base image
* Ensure the following commands execute:

~~~
"inline": ["echo 'Hello, World!' > index.html", "nohup busybox httpd -f -p 80 &" ], "inline_shebang" : "/bin/sh -x", "type" : "shell"
~~~

* Ensure that the resource group specified in packer for the image is the same image specified in Terraform


### Output
**Your words here**

