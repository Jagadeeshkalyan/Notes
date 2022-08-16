* Types of Applications:
	--> Web Applications/APIS
	--> Mobile Applications
	--> Standalone applications
	--> Data Storage:
		1. Big Data
			--> Hadoop
			--> Spark
		2. Datawarehouse & Data Mining
	--> AI/ML Applications
	--> IOT Applications
	--> Main frame

* Core Services Offered by Azure:
	--> Azure Virtual Machines: Need to worry about os, Deploy in VM
	--> Azure App Service: Direct deploy
	--> Azure Kubernetes Service
	--> Databases:
		1. SQL:
			--> SQL Server
			--> mySQL
			--> Postgres
		2. NoSQL
			--> Cosmos DB
		3. Cache
			--> Azure Redis Cache
		4. DataWareHouse
			--> Azure Synapse Analytics

* Azure Management Tools:
	--> Different interfaces for Azure:
		1. Browser Based => Using portal
		2. Terminal Based => Azure CLI / Azure Powershell
		3. SDK => Azure SDK

* We Manage
	--> Code
	--> App Service Plan => pricing & features

* Azure Manages
	--> VM Creation
	--> OS updates
	--> software updates
	--> Installing application dependencies

* Azure App Service is Platform as a Service (PaaS) solution that microsoft offers to assist developing your applications, mobile app back ends, 
or REST APIs or Web Applications without worrying about the underlying infrastructure.

* Azure App Service allows to host the applications from following languages directly
	--> .NET
	--> .NET Core,
	--> Java
	--> Node.js
	--> PHP
	--> Python
	--> Ruby

* Azure app service also allows to run docker containers in app service, which makes the way for any other web application in possibly any 
technology to run on Azure App Service.

* Azure App Service provides infrastrucutre capabilities such as load balancing, autoscaling, security, automated management.

* Azure App Service deployment can be integrated with Docker Hub, GitHub and Azure DevOps

* App Service Plan defines a set of computing resources for web app to run

* Each App Service Plan defines
	--> Operating System (Windows, Linux)
	--> Region (West US, East Us etc)
	--> Number of VM Instances
	--> Size of VM Instances (Small, Medium, Large)
	--> Pricing Tier (Free, Shared, Basic, Standard, Premium, PremiumV2, PremiumV3, Isolated, Isolated V2)

* Few categories of pricing tier:
	1. Shared Compute:
		--> Free and Shared, the two basic tiers runs app on the same Azure VM as other Azure Service apps, including apps of other 
		customers.
		--> These tiers allocate CPU quotas to each app that runs on shared resources
	2. Dedicated Compute:
		--> Basic, Standard and Premium tiers apps on dedicated Azure VMs.
		--> Only the apps in the Same Azure App Service plan can share the computing resources.
		--> The higher the tier, the more number of VM instances are available for scaling out.
	3. Isolated:
		--> The Isolate tier runs dedicated Azure VMs on dedicated Azure Virtual Networks.
		--> It provides network isolation on top of compute isolation to your applications.
		--> It provides the maximum scale-out capabilities.

