* Databases in Applications:
	1. Relational Databases:
		--> Data is represented in the form of Tables (Rows & Columns)
		--> There can be relations between tables
		--> Most of the applications still use Relational Databases
		--> To Create, Retrieve, Update and Delete (CRUD) we have a SQL (Structured Query Language)
		--> Popular Relational Database Management Systems (RDMBS)
			* Oracle
			* Microsoft SQL Server
			* mySql
			* PostgreSQL
	2. No SQL Database:
		--> This is type of Database which allows for storing wide variety of datasets
		--> This came into existense when the demand for modern applications increased.
		--> NoSQL Databases can further be divided into following categories
			* Key-Value Storage
			* Document Oriented Databases
			* Graph Databases
		--> Examples:
			* Mongo DB
			* Cassandra
			* Gremlin
			* Couchbase
	3. Cache Databases: 
		--> These are kind of databases which cache infrequently changed data into RAM for faster application Performances
		--> Examples:
			* Redis
			* Memcached
* Azure Database Offerings:
	1. Microsoft Azure has following Offerings:
		--> Relational Databases:
			* Azure SQL Database
			* Azure SQL Managed Instance
			* SQL Server on Azure Virtual Machines
			* Azure Database for PostgreSQL
			* Azure Database for MySQL/MariaDB
		--> No-SQL
			* Azure Cosmos DB
		--> Cache/In-memory Database:
			* Azure Cache for Redis
	2. Third Party VM Images (Azure MarketPlace):
		--> VM Images i.e using Images you can create VM with pre-existing software.

* Azure SQL Databases:
	--> It is fully managed database engine that handles most of the database management functions such as upgrading, patching, backups & 
	monitoring without user involvement.
	--> It always runs on the latest stable release of SQL Server database.
	--> It is not part of your vnet, you need to create a private endpoint to access azure sql database privately. 
	--> It Doesn't have all the features of SQL Server Enterprise and it will be difficult for customers who are using unsupported features 
	of Azure SQL to move to Azure SQL Database
	--> Deployment models:
		* Single Database: It represents a fully managed isolated database, you might use this option for modern cloud applications & microservices that need as single reliable datasource.
		* Elastic Pool: It represents collection of single databases with a shared set of resource such as CPU or memory. Single databases can be moved into and out of elastic pool.
	--> Purchasing Models:
		* vCore-based purchasing model:
			--> This model lets you choose the number of vCore, the amount of memory & speed of storage.
			--> The vCore-based purchasing model also allows you to use Azure Hybrid Benifit for SQL Server to gain cost savings.
			--> This is recommended model by Microsoft Azure.
		* DTU-based purchasing model:
			--> Database Transaction Unit offers a blend of compute, memory and I/O resource which supports light or heavy database 
			workloads.
		* Serverless model:
			--> This model automatically scales compute based on workload demand & bills for the amount compute per second.
			--> The serverless compute tier also automatically pauses the database during inactive periods when only storage is billed
			 and automatically resumes databases when activity returns.
	--> Service Tiers: Azure SQL Database offers three service tiers that are designed for different types of application workloads
		1. General Purpose/Standard:
			--> Designed for common workloads.
			--> offers budget oriented balanced compute and storage options.
		2. Business Critical/Premium:
			--> Designed for Online Transaction Processes (OLTP) applications with high transaction rate & lowest latency I/O.
			--> This offers highest resilience to failures by using several isolated replicas.
		3. HyperScale:
			--> Designed for very large OLTP database & ability to autoscale storage and scale compute fluidly.

* A Server is a logical construct that acts as a central administrative point for collection of databases where you can administer
	--> logins
	--> firewall rules
	--> auditing rules
	--> Threat detection policies
	--> Auto-failover groups

* Azure SQL Managed Instance:
	--> This is fully compatible with on-prem SQL Server.
	--> The Azure SQL Managed instance is part of the virtual network.
	Similarities between Azure SQL Database and Azure SQL Managed Instance
	----------------------------------------------------------------------
	--> Managment: Both will have support for
			* automated patching and version updates
			* automated backups
			* high availability
	--> Back up: Both supports automatic backup
			* Full backups are taken every 7 days
			* differntial backups 12 hours
			* log backup every 5-10 mins
			* Backup retention is 7 days default & max 35 days
	--> Availability: 99.99-99.995% availability is guaranteed for every database
	--> SQL MI: 99.99% availability is guranteed for every database
	--> Host Accessibility: There is no direct control over underlying compute server.
	--> License: Both have built-in license model with Pay as You go
	---------------------------------------------------------------------
	Key Differences between Azure SQL Database and Azure Managed Instance
	---------------------------------------------------------------------
	--> Recovery Model:
		* Azure SQL Database: From automated backup only
		* Azure SQL Managed Instance: From automated backups and full backups placed on Azure Blob Storage
	--> Active Geo-replication:
		* Azure SQL Database: Supported. In all service tier apart from hyper scale
		* Azure SQL Managed Instance: Not Supported, Use Auto failover groups as an alternative solution
	--> Auto Scale:
		* Azure SQL Database: Only supported in Serverless
		* Azure SQL Managed Instance: Not Supported
	--> Automatic tuning:
		* Azure SQL Database: Supported
		* Azure SQL Managed Instance: Not Supported
	--> Long Term Backup Retention:
		* Azure SQL Database: Supported, keep automatically taken backups for up to 10 years
		* Azure SQL Managed Instance: Use Manual backups as a work around

* Azure Database for MySQL:
	--> Azure Database for MySQL is a relational database service offered by Azure:
	* Zone redund and same zone high availability
	* Data protection using automatic backups and point in time restore for up to 35 days
	* Automatic patching and maintenance for underlying hardware, os and database engine
	* Predicatable performance
	* Monitoring and automation to simplify management for large scale deployments
	--> Azure Database for MySql is available in two deployment models
	1. Flexible Server:
		* This architecture allows users to opt for high availability within single AZ and across multiple AZ
		* Flexible Servers provide better cost optimization controls with the ability to stop/start server.
		* Reservations for Flexibile server allows users to save cost upto 63%
		* Suited for:
			--> Ease of deployments, simplified scaling & low database management overhead for functions like backups, HA, security 
			and monitoring
			--> Application developments requiring community version of MySQL
			--> Enterprise Grade Security
	2. Single Server:
		* This is fully managed MySQL designed for minimal customization.
		* The single server platform is designed to handle most of the database management functions such as patching, backups, minimal 
		user configuration
		* The architecture is optimized for built-in HA with 99.99%
		* Suited for:
			--> Existing applications already leveraging single server.
			--> Recommends flexible server deployment

* Azure Database for PostgreSQL: 
	--> Azure Also offers single server and flexible server for PostgreSQL
	--> With Azure Database for MySQL, Postgres ensure you select private access and add your vnet where your applications are running for 
	private connectivity

---------------------------------------
Difference Between MySQL and PostgreSQL
---------------------------------------

* Definition:
	--> MySQL is an open source Relational Database Management system (RDBMS). 
	--> PostgreSQL, on the other hand, is an open source Object Relational Database Management System (ORDBMS) with an emphasis on 
	extensibility and standards compliance.

* Developer:
	--> Oracle Corporation developed MySQL 
	--> PostgreSQL Global Development Group developed PostgreSQL.

* Data types:
	--> MySQL supports SQL standard data types
	--> PostgreSQL supports advanced data types such as arrays and user-defined types.

* Written Language:
	--> MySQL is written in C and C++
	--> PostgreSQL is written in C

* GUI Tool:
	--> The GUI tool of MySQL is MySQL workbench 
	--> The GUI tool of PostgreSQL is PgAdmin

