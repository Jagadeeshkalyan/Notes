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