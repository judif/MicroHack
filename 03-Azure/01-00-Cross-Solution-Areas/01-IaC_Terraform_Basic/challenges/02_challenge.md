# Challenge 2 - creating a virtual network

## **Introduction**
A virtual network is the fundamental building block for private networks in Azure. Azure Virtual Network enables Azure resources like VMs to securely communicate with each other, the internet, and on-premises networks.


## **Goal**

In this exercise, you will create a Virtual Network with two subnets, deploy Azure Bastion to securely connect to the VMs from the internet, and start private communication between the VMs you will create in Challenge 3.

## **Actions**

### Task 1: Create a VNet and an Azure Bastion host

Create a VNet with following criterias:
Name: microhack-vnet **//string**
Address space: 10.0.0.0/16 **//list**
Location: germanywestcentral **//string**
Resource Group Name: iac-microhack-rg **//string**

**Tipp:** Hier https://developer.hashicorp.com/terraform/language/expressions/types#string kannst du dir die Syntax der verschiedenen Typen in Terraform anschauen.

Insert the values above into the construct:
resource "azurerm_virtual_network" "iac_vnet" {
  name                = 
  address_space       = 
  location            = 
  resource_group_name =
}

// Create a virtual network
resource "azurerm_virtual_network" "iac_vnet" {
  name                = "iac-microhack-vnet"
  address_space       = ["10.0.0.0/16"]
  location            = "germanywestcentral"
  resource_group_name = azurerm_resource_group.rg.name
}

### Task 2: Deploy Azure Bastion with two Subnets
In this task you have to create a virtual network with a resource subnet, an Azure Bastion subnet, and a Bastion host.

- Subnets
    Segments of a virtual network's IP address range where you can place groups of isolated resources.

#### Subnet 1

Name: AzureBastionSubnet **//string**
Starting address: Use the default of 10.0.0.0.
Subnet size: Use the default of /24 (256 addresses)
Resource group name: iac-microhack-rg **//string**
Virtual network name: iac-microhack-vnet **//string**
![Alt Text]("C:\Users\lpaglionico\OneDrive - Microsoft\Dokumente\Dokumente\Workshops\IaC MicroHack\Subnet Settings.png")

Some supported arguments:
- name - (Required) The name of the subnet. Changing this forces a new resource to be created.

- resource_group_name - (Required) The name of the resource group in which to create the subnet. Changing this forces a new resource to be created.

- virtual_network_name - (Required) The name of the virtual network to which to attach the subnet. Changing this forces a new resource to be created.

- address_prefixes - (Required) The address prefixes to use for the subnet.

 - private_endpoint_network_policies_enabled - (Optional) Enable or Disable network policies for the private endpoint on the subnet. Setting this to true will Enable the policy and setting this to false will Disable the policy. Defaults to true.

 - service_endpoints - (Optional) The list of Service endpoints to associate with the subnet. Possible values include: Microsoft.AzureActiveDirectory, Microsoft.AzureCosmosDB, Microsoft.ContainerRegistry, Microsoft.EventHub, Microsoft.KeyVault, Microsoft.ServiceBus, Microsoft.Sql, Microsoft.Storage, Microsoft.Storage.Global and Microsoft.Web.

resource "azurerm_subnet" "iac_subnet_1_bastion" {
}

### Subnet 2
resource "azurerm_subnet" "iac_subnet_2_vm" {
  name                 = "vm-subnet"
  resource_group_name  = azurerm_resource_group.rg.name
  virtual_network_name = azurerm_virtual_network.my_terraform_network.name
  address_prefixes     = ["10.0.1.0/24"]
}

### Create Public IP for Azure Bastion

Some supported arguments:
- name - (Required) Specifies the name of the Bastion Host. Changing this forces a new resource to be created.

- resource_group_name - (Required) The name of the resource group in which to create the Bastion Host. Changing this forces a new resource to be created.

- location - (Required) Specifies the supported Azure location where the resource exists. Changing this forces a new resource to be created. Review Azure Bastion Host FAQ for supported locations.

Name: iac-microhack-bastion-pip **//string**
Location: germanywestcentral **//string**
Resource group name: iac-microhack-rg **//string**
Allocation methos: Static **//string**
Sku: Standart **//string**

resource "azurerm_public_ip" "iac_bastion_public_ip" {

}
### Deploy Bastian Host

When you have multiple subnets within your virtual network, you can choose to deploy Azure Bastion in one of these subnets.
The **AzureBastionSubne**t is the dedicated subnet where the Bastion host resides.

Some supported arguments:
- name - (Required) Specifies the name of the Bastion Host. Changing this forces a new resource to be created.

- resource_group_name - (Required) The name of the resource group in which to create the Bastion Host. Changing this forces a new resource to be created.

- location - (Required) Specifies the supported Azure location where the resource exists. Changing this forces a new resource to be created. Review Azure Bastion Host FAQ for supported locations.

- sku - (Optional) The SKU of the Bastion Host. Accepted values are Basic and Standard. Defaults to Basic.

- ip_configuration - (Required) A ip_configuration block as defined below. Changing this forces a new resource to be created.

A ip_configuration block supports the following:

- name - (Required) The name of the IP configuration. Changing this forces a new resource to be created.

- subnet_id - (Required) Reference to a subnet in which this Bastion Host has been created. Changing this forces a new resource to be created.

- public_ip_address_id - (Required) Reference to a Public IP Address to associate with this Bastion Host. Changing this forces a new resource to be created.

Name: iac-microhack-bastion-host **//string**
Location: germanywestcentral **//string**
Resource group name: iac-microhack-rg **//string**
    IP Configuration
    Name: iac-microhack-ip-configuration
    Subnet ID: azurerm_subnet.iac_subnet_1_bastion.id
    PIP ID: azurerm_public_ip.iac_public_ip.id


resource "azurerm_bastion_host" "iac_bastion_host" {

    ip_configuration {

    }
}
