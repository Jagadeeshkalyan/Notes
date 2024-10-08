* Docker is an open platform for developing, shipping, and running applications.

* During peak hours only few components of our applications might be busy, but we scale the whole application which increase the amount of hardware resources such as CPU, RAM, Storage etc unnecessarily. This thought process has lead us to microservices (scaling individual service components).

* Docker enables you to separate your applications(microservices) from your infrastructure so you can deliver software quickly.

* Containers are used to run our application effectively.

* Docker images are required to create containers. From one Docker image, we can create multiple containers. Images are build-time constructs and containers are run-time constructs.

* Docker image is collection of Image Layers. Each layer has it's own unique id.

* Two different images having the same image id imply that they are same images with different names.

* Docker Technology: 
	* Three things to be aware of when we are referring to docker as a technology:
		1. The runtime:
			--> runc: Lower level runtime(on per running container)
			--> containerd: Higher level runtime(talks to runc instance)
		2. The daemon/Engine:
			--> Remote API
			--> Networking
			--> Volume
			--> Image mgnt
			--> Others
		3. The orchestrator:
			--> Swarm: manages cluster of Docker nodes

* Responsibility of a DevOps Engineer:
	As per the understanding of docker which we have so far, We need to create containers which run the applications developed by our organization. The first responsibility of DevOps Engineer to
	--> Create a Docker Image which has your application preconfigured.
	--> Manage multiple versions of your Docker Image.
	--> Store the Images in Organization approved Registry.

* Docker by default runs in the attached mode where it uses your terminal for showing standard output/standard errors from container.

* We can execute any command inside the running contianer 
  "docker container exec <container name/id> <command>".

* Container can be defined as isolation with some resource limits.

* Isolations on the linux machines are created using a linux kernel feature called Namespaces. 

* Resource Limits are applied using kernel feature called as cgroups (Control groups).

* Namespaces: Namespaces is a linux feature.
	* pID namespace (Process Namespace): It creates the isolated process tree inside container.
	* net namespace (Network Namespace): It creates the isolated networking for each container with its own network interface.
	* Mount Namespace: It allows each container to have a different view of entire systems mount point, this allows containers to have their own file system view which starts from root.
	* User Namespace: It allows a process to have root privileges within the namespace, without giving it that access to processes outside of the namespace.
	* IPC Namespace: Isolating a process by the IPC namespace gives its own interprocess communication resources.
	* UTS Namespace(UNIX Time-Sharing): It isolates two specific identifiers of the system: nodename and domainname.

* Control group (cgroup) Namespace: 
	--> cgroups is a linux kernel feature.
	--> Control groups is used to impose limits. We can impose limits of disk io, RAM & cpu�s using ControlGroups.

* Docker has built a project called as libcontainer and the goal of libcontainer was to provide Docker with building blocks that exist in the host kernel to create containers.

* Open Container Initiative(OCI): 
	--> It is an open governance structure for the express purpose of creating open industry standards around container formats and runtimes.
	--> The OCI standards came up with two specifications:
		1. Image spec 
		2. Container runtime spec 

* Docker images are required to create containers.
* From one Docker image, we can create multiple containers.
* Images are build-time constructs and containers are run-time constructs.
* Docker image is collection of Image Layers.
* Whenever we make changes that leads to some changes in the file system (RUN, ADD) then a new layer is gets created.

Docker image Registry:
----------------------
* The Default Registries is DockerHub.
* There are many other Registries to Store docker images
	* Cloud Registries:
		1. Azure Container Registry
		2. AWS ECR
		3. Docker Hub (Public and Private) And many other
	* Hosted Registries:
		1. Artifactory/Jfrog
		2. We can also use Docker Registry Image to store our images Share
* The basic instructions are
	FROM => Helps in choosing the base image
	RUN => Adds the execution/installation on the base image to build our application
	LABEL => ADDS metadata
	ENV => Set ENVIRONMENT variables
	EXPOSE => PORTS to be exposed by application
	ADD/COPY => Content to be added into the image from local or from urlss
	USER => User with which container has to be started (if not specificed root)
	WORKDIR => Working Directory
	ARG => Build time arguments
	CMD => Command that will be called when container is created whatever is written in CMD can be overriten
	ENTRYPOINT => Command that will be called when container is created and cannot be overriten 

* docker build  -t ImageName:TagName dir
  * Options
  -t − is to mention a tag to the image
  ImageName − This is the name you want to give to your image.

  TagName − This is the tag you want to give to your image.

  Dir − The directory where the Docker File is present.

* -p is used to map the port number

* The images in docker hub are stored in repositories with each repository having a name <acount-username>/<image-name>
* To push nop commerce i need to have my image in the form of shaikkhajaibrahim/nop
* Now lets tag nop to the new naming convention 
  ```
  docker image tag nop shaikkhajaibrahim/nop:1.0
  ```
* Now push
  ```
  docker image push shaikkhajaibrahim/nop:1.0
  ```
* "--rm" argument specifies that the container should be removed when you stop it.
### ACR
* An Azure container registry stores and manages private container images and other artifacts.
* Docker Hub stores public Docker container images.
* Azure container registry - Create a container registry in your Azure subscription.
  * Azure portal: 
    * Now lets try to creat an Azure Container registry and push the nop image to it
	```
	container registry --> create container registry
	```
    * enter values for Resource group and Registry name and location
    * Basic --> Networking --> Encryption --> Tags --> Review+create
    * Take note of the registry name and the value of the Login server, which is a fully qualified name ending with azurecr.io in the Azure cloud. You use these values in the following steps when you push and pull images with Docker.
  * Log in to registry:
    * Before pushing and pulling container images, you must log in to the registry instance.
    ```
	az acr login --name <registry-name>
	``` 
	* To push an image to an Azure Container registry, you must first have an image. If you don't yet have any local container images, run the following
	```
	docker pull mcr.microsoft.com/hello-world
	docker tag mcr.microsoft.com/hello-world <login-server>/hello-world:v1
	docker push <login-server>/hello-world:v1
	docker rmi <login-server>/hello-world:v1
	```
	* docker rmi command does not remove the image from the hello-world repository in your Azure container registry. removes the image from  local Docker env.

	https://www.tutorialspoint.com/docker/docker_continuous_integration.htm