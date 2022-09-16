Infrastructure as code (IAC):
----------------------------
* Is to write & execute the code to define, deploy, update and destroy your infrastructure.
* vcs -> Bulid/package -> Terraform -> Environment 
* 1. System test Environment
  2. performance test Environment
  3. UAT/Pre-prod
  4. Production
* The major concepts of terraform are
    Provider:
        Where we can create infrastructure
    Resource:
        What has to be created
    DataSource:
        Query information about anything in the Provider

###Why Terraform
--------------- 
* Orchestration:
    * It concentrates more on server provisioning with software container deployment left to Docker and Packer
* Immutable infrastructure: 
    * Very new update of any parameter creates a separate configuration snapshot
    * By this we can achieve bug free and environment go smoothly
* Declarative code:
    * code is small and easily understandable
* Client-Only architecture:
    * Cloud providers API for provisioning the infrastructure which removes the need of additional security checks, running the separate configuration management server and multiple software agents.

### Working with Terraform
* Identify the infrastructure you need to create/provision
* Identify the providers
* Configure the provider using HCL (Hashicorp Configuration Language)
* Configure the resources to be created using HCL


What is Terraform
-----------------
* Terraform is an open source infrastructure-as-a-code tool developed by Hashicorp where we can store our cloud infrastructure setup as codes.
* 

### Terraform Workflow
----------------------
* Init
* Validate
* Plan
* Apply
* Destroy

* The two major elements in the Terraform language are
  * Arguments:
    * Assigns a value to a particular name "resource name = value"
  * Blocks:
    * A block is container for other content
    * Three major blocks of terraform are
      * provider block
      * resource block
      * datasource block

### Provider block
* Basic Syntax for aws provider
  ```
  provider "<provider-name>" {
    <argument-1>
    <argument-2>
    ..
    <argument-n>
  }
  ```
* Example
  ```
  provider "aws" {
    access_key  = "LKJLKSKLJDALDJLKSADSLA"
    secret_key  = "lksdfjdlkasfjlsadfjlksdafjlksdafjdallksafj"
    region      = "ap-south-1"
  }
  ```
* Basic Syntax for azure provider
  ```
  # We strongly recommend using the required_providers block to set the
  # Azure Provider source and version being used
    terraform {
      required_providers {
        azurerm = {
          source  = "hashicorp/azurerm"
          version = "=3.0.0"
        }
      }
    }
  # Configure the Microsoft Azure Provider
    provider "azurerm" {
       features {}
    } 
  ```
### Resource Block
* Basic Syntax
  ```
  resource "<PROVIDER>_<TYPE>" "<NAME>" {
    <argument-1>
    <argument-2>
    ..
    <argument-n>
  }
  ```
* Example
 ```
  resource "aws_s3_bucket" "b" {
  bucket = "qt-tf-s3-1"

  tags = {
    Name        = "My bucket"
    Environment = "Dev"
  }
 }
 ```
* The inputs provided to the Resources/Datasources is called as arguments and the outputs are referred as attributes.
* When terraform commands are executed generally they scan all the .tf files in the directory and execute the configuration.
* Lets define the provider and vpc definition
```
  provider "aws" {
    access_key  = "LKJLKSKLJDALDJLKSADSLA"
    secret_key  = "lksdfjdlkasfjlsadfjlksdafjlksdafjdallksafj"
    region      = "ap-south-1"
  }
  # lets try to define the resource for the vpc (vpc is similar to vnet in azure)
  resource "aws_vpc" "myvpc" {
    cidr_block = "192.168.0.0/16"

    tags = {
      "Name" = "from-tf"
    }
 }
```
* Now perform init and validate. Now lets apply terraform to create infra terraform apply
* The vpc id is the attribute of the resource block to access attributes the syntax is <PROVIDER>_<TYPE>.<NAME>.<ATTRIBUTE-NAME>
```
# lets create web1 subnet
resource "aws_subnet" "web1" {
    vpc_id              = aws_vpc.myvpc.id
    cidr_block          = "192.168.0.0/24"
    availability_zone   = "ap-south-1a"

    tags                = {
      "Name"            = "web1-tf"
    }

}

# lets create web2 subnet
resource "aws_subnet" "web2" {
    vpc_id              = aws_vpc.myvpc.id
    cidr_block          = "192.168.1.0/24"
    availability_zone   = "ap-south-1b"

    tags                = {
      "Name"            = "web2-tf"
    }

}
```
### Declaring an Input Variable
* Each input variable accepted by a module must be declared using a variable block
* Terraform CLI defines the following optional arguments for variable declarations:
  * default - A default value which then makes the variable optional.
  * type - This argument specifies what value types are accepted for the variable.
  * description - This specifies the input variable's documentation.
  * validation - A block to define validation rules, usually in addition to type constraints.
  * sensitive - Limits Terraform UI output when the variable is used in configuration.
  * nullable - Specify if the variable can be null within the module.
* Now declaring variables. Syntax is <variable> <"name of the variable">
```
variable "target_region" {
    type        = string
    default     = "ap-south-1"
    description = "region where the infra can be created"
}

variable "vpc_cidr_range" {
    type        = string
    default     = "192.168.0.0/16"
    description = "cidr range of vpc"
```
* Now in .tf file the configuration will be as
```
provider "aws" {
    access_key  = "LKJLKSKLJDALDJLKSADSLA"
    secret_key  = "lksdfjdlkasfjlsadfjlksdafjlksdafjdallksafj"
    region      = var.target_region
  }
  # lets try to define the resource for the vpc (vpc is similar to vnet in azure)
  resource "aws_vpc" "myvpc" {
    cidr_block = "var.vpc_cidr_range"

    tags = {
      "Name" = "from-tf"
    }
 }
```
* Now validate the terraform script "terraform validate"
* To pass the variables from command line
```
terraform apply -var="target_region=us-west-2" -var="vpc_cidr_range=10.0.0.0/16"
``` 
* Variables on the Command Line
```
terraform apply -var="image_id=ami-abc123"
terraform apply -var='image_id_list=["ami-abc123","ami-def456"]' -var="instance_type=t2.micro"
terraform apply -var='image_id_map={"us-east-1":"ami-abc123","us-east-2":"ami-def456"}'
```
* To set lots of variables, it is more convenient to specify their values in a variable definitions file (with a filename ending in either ".tfvars" or ".tfvars.json") and then specify that file on the command line with -var-file.
```
terraform apply -var-file="testing.tfvars"
```
### Variable file
* Creating variables.tfvars file and adding variables values
```
target_region = "ap-south-1"
vpc_cidr_range = "192.168.0.0/16"
```
* Now use apply command
```
terraform apply -var-file "variables.tfvars"
```
* We can add default variables in default.tfvars
```
target_region   = "ap-south-1"
vpc_cidr_range  = "192.168.0.0/16"
web1_cidr_range = "192.168.0.0/24"
web2_cidr_range = "192.168.1.0/24"
db1_cidr_range  = "192.168.2.0/24"
db2_cidr_range  = "192.168.3.0/24"
web1_az         = "ap-south-1a"
web2_az         = "ap-south-1b"
db1_az          = "ap-south-1a"
db2_az          = "ap-south-1b"
```
* inputs.tf
```
variable "vpc_cidr_range" {
    type        = string
    description = "cidr range of vpc"

variable "web1_cidr_range" {
    type        = string
    description = "cidr range of web1 subnet"
}

variable "web2_cidr_range" {
    type        = string
    description = "cidr range of web2 subnet"
}

variable "web1_az" {
    type        = string
    description = "az of web1 subnet"
}

variable "web2_az" {
    type        = string
    description = "az of web2 subnet"
}


variable "db1_cidr_range" {
    type        = string
    description = "cidr range of db1 subnet"
}

variable "db2_cidr_range" {
    type        = string
    description = "cidr range of db2 subnet"
}

variable "db1_az" {
    type        = string
    description = "az of db1 subnet"
}

variable "db2_az" {
    type        = string
    description = "az of db2 subnet"
}
```
### Example
* Create the vpc, 6 subnet(3 in az1 and 3 in az2), s3 bucket
* Create the internet gateway and attach to the vpc
* Solution:
  * created three files
    1. provider.tf
    2. input.tf
    3. network.tf

1. provider.tf:
```
provider "aws" {
    region = var.region
}
```
2. input.tf:
```
variable "region" {
    type = string
    default = "us-west-2"
}

variable "availability_zone_1" {
    type = string
    default = "us-west-2a"
}

variable "avaiablity_zone_2" {
    type = string
    default = "us-west-2b"
}

variable "vpc_cidr_range" {
    type = string
    default = 10.0.0.0/16
}

variable "subnet_cidr_range" {
    type = list (string)
    default = {"10.0.0.0/24", "10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24", "10.0.4.0/24", "10.0.5.0/24"}
}

variable "bucket_name" {
    type    = string
    default = "qts3khajatf3"
}
```
3. network.tf: 
   [referhere] https://github.com/asquarezone/TerraformZone/commit/538f2f4085409fdb7624ffe232be08a69e4c9b10#diff-9a9cf4b27d314b7514081b3135b17f7f7acdfda4d0a875a823a0bd24e8b1b0d9

### Variable types
* variable types supported by terraform are
  * string
  * number
  * bool
  * list
  * map
  * set
  * object
  * any

* Terraform offers loops
  * loops with count paramter:
    * you can use count.index to get the index of each “iteration” in the “loop”:
```
resource "aws_iam_user" "example" {
  count = 3
  name  = "neo.${count.index}"
}
```
  * For example, you could define all of the IAM usernames you want in an input variable called user_names:
```
variable "user_names" {
  description = "Create IAM users with these names"
  type        = list(string)
  default     = ["neo", "trinity", "morpheus"]
}
```

  [referhere] https://github.com/asquarezone/TerraformZone/commit/4cba883dccbebcfe6ecb9ea97a227cc3aa851331?diff=split#diff-9a9cf4b27d314b7514081b3135b17f7f7acdfda4d0a875a823a0bd24e8b1b0d9
  * loops with for_each expression
  * loops with for expression

### Terraform State
* Terraform maintains the information of resources created in the state file.
* This file contains a custom JSON format that records a mapping from the Terraform resources in your configuration files to a representation of those resources in the real world (Provider).
* When we execute terraform apply, terraform first fetches the information from provider about the resources in state file and compares that to the state file, if there any changes required to match what you want (expressed) in your configuration file, terraform executes them
* Azure provider: [referhere]https://github.com/asquarezone/TerraformZone/commit/b8326aed9faa8f37f22ac19a50375449378dc1e1#diff-97112977697e93f213ec193fc40148374d79972ae51163a48ae4b1c7858c5585

### Local variable
* Local values can be helpful to avoid repeating the same values or expressions multiple times in a configuration, but if overused they can also make a configuration hard to read by future maintainers by hiding the actual values used.

* when we apply terraform apply the plan gets created internally, we can create the plan externally as well.
* Now execute `terraform plan -out “myfirstplan”
* When we have a small fix then use the command
  ```
  terraform apply -auto-approve
  ```

### Provisioner types:
* file
* local-exec
* remote-exec
* chef
* salt
* puppet

* A backend defines where Terraform stores its state data files.










* IAC or Infrastructure as Code allows you to build, change, and manage your infrastructure through coding instead of manual processes. The configuration files are created according to your infrastructure specifications and these configurations can be edited and distributed securely within an organization.
* Vcs ---> Build/package ---> Terraform ---> testing 
* Strings, numbers, and bools are sometimes called primitive types. Lists/tuples and maps/objects are sometimes called complex types, structural types, or collection types.
* null: a value that represents absence or omission. If you set an argument of a resource to null, Terraform behaves as though you had completely omitted it

