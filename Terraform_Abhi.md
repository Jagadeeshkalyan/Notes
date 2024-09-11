Terraform (IAC):
Build and maintain infrastructure as a code through Terraform
Terraform flow:
terraform init - intialize a provider
terraform plan - a dry run, Describe the infrastructure
terraform apply - deploy the infrastructure

- How do Terraform authenticate to AWS
    aws configure
        enter accesskey id
        enter secret key id
        enter default region name
        enter default json format

Scenario 1:
maintain terraform files in github, create a remote backend to store terraform state file and integrate a proper locking mechanism using Dynamodb.
    - S3: remote backend (tfstate file maintains the infrastructure and terraform relies on tfstate regarding infrastructure)
    - Dynamodb: create a lock for tfstate file and will not allow parallel execution.


Modules:
