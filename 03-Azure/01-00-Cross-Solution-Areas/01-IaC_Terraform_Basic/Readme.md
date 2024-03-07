# **MicroHack - Terraform on Azure**

- [**MicroHack introduction**](#MicroHack-introduction)
- [**MicroHack context**](#microhack-context)
- [**Objectives**](#objectives)
- [**MicroHack Challenges**](#microhack-challenges)
- [**Contributors**](#contributors)

# MicroHack introduction

This MicroHack scenario provides a comprehensive guide on using Terraform on Azure, emphasizing best practices and design principles. This workshop will guide you through best practices, from initial resources and modules, to complex concepts and abstractions, to process aspects and the use of CI/CD with GitHub.

Before diving into the MicroHack, it is important to understand the concepts and objectives of Infrastructure as Code in particular Terraform. Go and checkout documentation and resources linked below:

- [Terraform on Azure](https://learn.microsoft.com/en-us/azure/developer/terraform/overview)
- [What is Terraform](https://developer.hashicorp.com/terraform/intro)

# MicroHack context

tbd

# Objectives

tbd

# MicroHack challenges

## General prerequisites

This MicroHack has a few but important prerequisites. In order to use the MicroHack time most effectively, the following tasks should be completed prior to starting the session.

Make sure your machine is equipped with the following tools:

- [Terraform](https://developer.hashicorp.com/terraform/tutorials/azure-get-started/install-cli)
- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
- [Visual Studio Code](https://code.visualstudio.com/download)

An Azure Subscription is required to complete the MicroHack. If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/) before you begin.

Permissions for the deployment or a Service Principal are required and would be helpful to have prepared before the MicroHack. If you don't have the necessary permissions, please reach out to your Azure Administrator to get the following permissions:

- Contributor on the subscription or resource group

## Challenge 1 - Getting started with Terraform

### Goal

In this exercise, you will create a Terraform configuration to deploy an Azure resource group. This resource group will serve as the base for the infrastructure you will construct in the following challenges.

### Actions

* Create a new file called `main.tf` in a new directory.
* Add the following code to the `main.tf` file:
    ```hcl 
    # Configure the Azure provider
    terraform {
        required_providers {
            azurerm = {
                source  = "hashicorp/azurerm"
                version = "~> 3.0.2"
            }
        }

        required_version = ">= 1.1.0"
    }

    provider "azurerm" {
        features {}
    }

    resource "azurerm_resource_group" "rg_iac" {
        name     = "rg-iac-microhack"
        location = "germanywestcentral"
    }
    ```
* Review and discuss each block of the code with the group.
  * Terraform Block - `terraform`
  * Provider Block - `provider "azurerm"`
  * Resource Block - `resource "azurerm_resource_group" "rg_iac"`
* Initialize the Terraform configuration by running `terraform init` in the directory where the `main.tf` file is located.
* Format and validate the Terraform configuration by running `terraform fmt` and `terraform validate`.
* Deploy the Terraform configuration by running `terraform apply` and confirm the deployment by typing `yes` when prompted.
* Inspection of the deployed resource group in the Azure Portal and the state file in the local directory.

### Success criteria

* You have deployed a resource group using Terraform.
* You have successfully initialized, formatted, and validated the Terraform configuration.
* Understanding of the Terraform configuration and the deployed resource group.

### Learning resources
* [Create an Azure resource goup](https://learn.microsoft.com/en-us/azure/developer/terraform/create-resource-group?tabs=azure-cli)
* [Terraform - Get Started on Azure](https://developer.hashicorp.com/terraform/tutorials/azure-get-started)

### Solution - Spoilerwarning

[Solution Steps](./walkthrough/challenge-1/solution.md)

## Challenge 2 - ...

### Goal 

The goal of this exercise is to deploy...

### Actions

* Write down the first 3 steps....
* Set up and enable...
* Perform and monitor....

### Success criteria

* You have deployed ....
* You successfully enabled ...
* You have successfully setup ....
* You have successfully ....

### Learning resources
* Link to https://learn.microsoft.com/en-us/azure/....

### Solution - Spoilerwarning

[Solution Steps](./walkthrough/challenge-2/solution.md)

## Finish

Congratulations! You finished the MicroHack *Name*. We hope you had the chance to learn about the how to implement a successful...
If you want to give feedback please dont hesitate to open an Issue on the repository or get in touch with one of us directly.

Thank you for investing the time and see you next time!


## Contributors
* Judith Freiberger - [GitHub](https://github.com/judif) & [LinkedIn](https://www.linkedin.com/in/judithfreiberger/)
* Nils Pinnau - [GitHub](https://github.com/nilspinnau) & [LinkedIn](https://www.linkedin.com/in/nils-pinnau-6a5ba3222/)
* Luise Paglionico - [GitHub](https://github.com/LuiseMaria) & [LinkedIn](https://www.linkedin.com/in/luise-paglionico/)
