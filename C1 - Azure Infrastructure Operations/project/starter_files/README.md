# Azure Infrastructure Operations Project: Deploying a scalable IaaS web server in Azure

### Introduction

This is the first project of the Azure DevOps nanodegree, where students must deploy a web server in Azure using terraform and packer.

### First Steps
1. Firstly, we need an [Azure Account](https://portal.azure.com) 
2. After getting an Azure account, we must install the [Azure command-line interface](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
3. To create and deploy the Virtual Machine (VM) image, we need [Packer](https://www.packer.io/downloads)
4. For automated creation of our infrastructure, we need to install [Terraform](https://www.terraform.io/downloads.html)

### Instructions

Before getting started, we must create a policy that ensures all indexed resources are tagged. This policy will help us with organization and tracking, making it easier to log when things go wrong. For this task, we should use the Azure Policy tool found inside the security center. According to the given specifications, the policy to be created should **deny** the creation of resources that **do not have tags**.  

There are many ways to accomplish this task, such as using the Azure Portal, Azure Command Line (CLI), or using Terraform. I chose the latter to make it scriptable. The policy is depicted below.

~~~
{
    "type": "Microsoft.Authorization/policyDefinitions",
    "name": "audit-existing-linux-vm-ssh-with-password", 
    "properties": {
        "mode": "all",
        "displayName": "Audit SSH Auth on Existing Resources",
        "description": "This policy audits whether any Linux VMs use password-only authentication for SSH on existing resources.",
        "policyRule": {
            "if": {
                "allof": [
                    {
                        "field": "type",
                        "equals": "Microsoft.Compute/virtualMachines"
                    },
                    {
                        "field": "Microsoft.Compute/virtualMachines/osProfile.linuxConfiguration",
                        "exists": "True"
                    },
                    {
                        "field": "Microsoft.Compute/virtualMachines/osProfile.linuxConfiguration.disablePasswordAuthentication",
                        "equals": "false"
                    }
                ]
            },
            "then": {
                "effect": "audit"
            }
        }
    }
}
~~~

### Output
**Your words here**

