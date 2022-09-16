* K8s takes care of
  1. Scaling requirements
  2. Failover
  3. Deployment Options

* K8S provides
  1. Service Discovery & Load Balancing
  2. Storage Orchestration
  3. Automated rollouts and rollbacks
  4. Self-Healing
  5. Secret and Configuration Management

* K8s Can be installed in many ways
  * Self Hosted => where we install k8s
    1. minikube
    2. Kubeadm
    3. Kube Spray
  * Cloud Hosted Services => Kubernetes as a Service
    1. AWS => Elastic Kubernetes Service (EKS)
    2. Azure => Azure Kubernetes Service (AKS)
    3. Google => Google Kubernetes Engine (GKE)

* K8s is a platform that manages container based applications, their network and storage components 
  * Master
  	* Provides Core K8S services and Orchestration Features
  	* Assigns work to be done on the Nodes
  * Node
    * Run your application Workloads
* K8S Architecture
  * Cluster master
    * *API Server*:
      * This component is Central to Kubernetes. All communications between all components goes through the kube-apiserver.
      * This component is frontend of the Kubernetes control plane.
      * This component exposes a REST API.
      * We would interact with this component using kubectl by using the YAML files, which are also referred as manifests.
    * *Scheduler*:
      * It watches for new work tasks and assigns them to healthy nodes in the cluster.
    * *etcd*:
      * etcd stores the entire configuration and the state of the cluster.
      * etcd is consistent and highly available distributed key-value store.
    * *Controller manager*:
      * It is responsible for maintaining desired states mentioned in the manifest.
      * It looks like single component, but with in it has
        * *Node Controller*: for noticing & responding when node goes down
        * *Replication Controller*: for maintaining the correct number of pods for every replication controller object.
        * *Endpoints Controller*: Populates the Endpoints object
  * *Node*
    * *Kubelet*: 
      * This is an agent which runs on each node in the cluster.
      * It watches for the instructions from API Server for new work assignments.
      * If it can’t run the task assigned, it reports back to master and lets control plane decide on the actions.
      * It is responsible for the node registration process
    * *Container runtime*:
      * This is software which is responsible for running containers.
      * Some of them are Docker, containerd, cri-o, rktlet.
    * *Kube proxy*:
      * Maintains the network rules on nodes
      * This is responsible for networking on nodes.
    * *Cluster DNS*:
      * Every Kubernetes Cluster has an internal DNS service
      * This has static IP address that is hardcoded into every Pod on the cluster i.e. all Pods now how to find the DNS Server
    * Services, Stateful Sets and Pods are registered with Cluster DNS.

* Using Hypervisors like hyper-v, vmware we create virtual machines, using docker we create containers. The Atomic unit of creation for Hypervisor is Virtual Machine and for Docker it is container.
* In K8S the atomic unit of Work is Pod.
* A Pod is group of one or more containers with shared network and storage resources.
* Kubectl, allows you to run commands against Kubernetes clusters. You can use kubectl to deploy applications, inspect and manage cluster resources, and view logs.
  ```
  kubectl run httpd --image httpd
  kubectl get pods
  kubectl get pods -o wide
  kubectl delete pods httpd
  ```
* Creating a pod using Yaml file by declarative approach. creating yaml file "vi test.yml"
  ```
  apiVersion: v1
  kind: Pod
  metadata:
    name: httpd
  spec:
    containers:
      - name: httpd
        image: httpd:latest
        ports:
          - containerPort: 80
  ```
* Create resource from yaml file
  ```
  kubectl apply -f test.yml
  kubectl get pods -o wide
  kubectl delete -f test.yml
  ```
* When working with kubectl we have two approaches
  * Imperative: To create our workloads we use commands.
  * Declarative: We define our desired file in a yaml file and provide the yaml file to the kubectl.
* The most basic command of viewing k8s objects is get.
  ```
  kubectl get <resource-name> => all resources 
  kubectl get <resource-name> <object-name> => to view the specific resource
  ```
* Creating pod and observing commands
  ```
  kubectl run httpd --image httpd
  kubectl get pods
  kubectl get po
  kubectl get pods httpd
  kubectl get pods httpd -o wide 
  ## All the above get commands give the same output
  ```
* kubectl cheatsheet: [Referhere]https://kubernetes.io/docs/reference/kubectl/cheatsheet/
* view the k8s object in the json or yaml format:
  ```
  kubectl get <resource-name> <object-name> -o json 
    kubectl get pods httpd -o json
  kubectl get <resource-name> <object-name> -o yaml
    kubectl get pods httpds -o yaml
  ```

### Kubernetes APIs & Objects:

* Kubernetes exposes different sets of REST APIs for different Purposes.
* These APIs serve as a foundation for the declarative configuration schema for the system, Which the kubectl tool uses to create, update, delete and get API Objects.
* Kubernetes also stores its serialized state in etcd in terms of the API Resources.
* Kubernetes APIs are in constant development, so Kubernetes follows the strict API Versioning & to simplify extending of APIs API groups are implemented.
  
API Versioning:
--------------
*  Kubernetes supports multiple API Versions, each at different API path such as api/v1 or /apis/extensions/v1beta1.
* Different API Versions imply different levels of stability & support.
  * Alpha level:
    * Version name consists of alpha e.g (v1alpha1)
    * May be buggy, These features are disabled by default
    * Support for feature may be dropped at any time without notice
    * API changes may be incompatible in later versions
  * Beta level:
    * Version name consists of beta e.g (v2beta3)
    * Code is well tested. These features are enabled by default
    * Support for overall feature will not be dropped, but details may change
  * Stable level:
    * Version name will in in the format of vX where x is an integer
    * Stable versions of features will appear in released software for many subsequent versions
    * To get all the available api versions in your Kubernetes cluster execute 
```
kubectl api-versions
```
API groups:
-----------
* API group is specified in the apiVersion field of the Kubernetes Object
* There are several API groups in use
  * core group: referred as legacy group. It is at the REST path api/v1 and uses apiVersion: v1
  * named groups: They are at the REST path /apis/$GROUP_NAME/$VERSION and use apiVersion: $GROUPNAME/$VERSION e.g (apiVersion: batch/v1)

Kubernetes Objects:
-------------------
* Kubernetes Objects are persistent entities in Kubernetes. Kubernetes uses these entities to represent state of your cluster
* They can describe
  * What containerized applications are running (and On which nodes)
  * Resources available to those applications
  * Policies around how those applications behave
* You can work with Kubernetes Objects for create, modify and delete using
  * kubectl cli
  * API Directly from Client Libraries
* Every Kubernetes object includes two nested object fields that govern the configuration
  1. Object Spec:
    * In this you need to describe the desired state for the object.
    * Can be considered as input 
  2. Object Status:
    * Actual status of the object supplied by Kubernetes system
    * Can be considered as output

Required Fields in the .yaml file for the Kubernetes object:
------------------------------------------------------------
* apiVersion - Which version of the Kubernetes API you're using to create this object
* kind - What kind of object you want to create
* metadata - Data that helps uniquely identify the object, including a name string, UID, and optional namespace
  1. Names:
  * All objects in the Kubernetes REST API are identified by Name and UID (Unique Identifier)
  * Only one object of a given kind can have a given name at a time. If you delete the object , you can make a new object with same name.
  * Max length of 253 characters
  * Generally lower case alphanumeric characters, – and .
  * In the below example tomcat-demo is for Pod name and tomcat for Container name
  ```
  apiVersion: v1
  kind: Pod
  metadata:
    name: tomcat-demo
  spec:
    containers:
    - name: tomcat
      image: tomcat:8
      ports:
      - containerPort: 8080
  ```
  2. UIDs:
  * Kubernetes systems-generated string to uniquely identify objects.
  ```
  kubectl get <object> -o yaml | grep uid
  ```
* spec - What state you desire for the object

Kubernetes Workloads:
---------------------
* Kubernetes Workloads are classified as Pods & Controllers.
* *pods*:
  * It is atomic unit of Kubernetes Application.
  * Pod has Container(s), Storage resources, a unique Network IP
  * In Kubernetes Pods can be created directly.
  * Pod workloads do not maintain desired state, But controllers can.
  * If you are running multiple containers in the Pod, they share same IP Address and port space, have the same host name and can communicate over IPC.
  * Pods are describe by declarative Pod manifest.
  * Since Pod is a Kubernetes Object, it will have Object Spec and Status.
  * [ReferHere]https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#pod-v1-core
  * create a file name tomcat-pod.yml with below content
  ```
  apiVersion: v1
  kind: Pod
  metadata:
    name: tomcat
  spec:
    containers:
      - image: tomcat:8
        name: tomcat
        ports:
          - containerPort: 8080
            name: http
            protocol: TCP
  ```
  * Execute below commands and observe the results
  ```
  kubectl apply -f tomcat-pod.yml
  kubectl get pods
  kubectl get pods tomcat
  kubectl describe pods tomcat
  kubectl port-forward tomcat 8080:8080
  kubectl exec tomcat date
  kubectl delete -f tomcat-pod.yml
  ```
* *Controllers*
  * Available Controllers are
    * ReplicaSet
    * ReplicationController
    * Deployments
    * StatefulSets
    * DaemonSet
    * CronJob

```
kubectl apply -f activity.yml
kubectl get po -o wide
kubectl exec -it activity --/bin/sh
kubectl describe pods activity
kubectl port-forward --address "0.0.0.0" activity 8080:80
kubectl logs activity
```
* If we try to use the above workloads then the desired state is maintained
* Since Pod cannot maintain its own state i.e. if the Pod is Down, schedule the Pod on a new node
* Running our application in the Workload resources which maintain some kind of desired state is what we want.
* Before we understand workload resources, we need to understand the concept of labels and annotations in kubernetes

Labels:
-------
* Labels are key/value pairs that can be attached to k8s objects such as Pods, replicasets etc.
* They are arbitrary and are useful for identifying information about k8s objects
* They provide the foundation for grouping objects
* Labels have very simple syntax.
* Keys can be broken down into two parts an optional prefix and a name seperated by slash (dots, underscores, dashes(hypens)) can be used in names
* Values are strings with maximum of 63 characters
| key | value |
| — | ——|
| qt.com/app-version | 1.0.0 |
| appVersion | 1.0.0 |
| app.version | 1.0.0 |
| project | qtidentitiy |
* Lets try to apply labels
  ```
  kubectl run nginx-prod --image=nginx --labels="version=1.0.0,app=web,env=prod"
  kubectl run nginx-prod --image=nginx --labels="version=1.1.0,app=web,env=test"
  kubectl get pods --show-labels
  ```
* Label Selectors: These are used to filter k8s objects based on set of labels
  ```
  kubectl get pods --selector="app=web"
  kubectl get pods --selector="app=web" --show-labels
  kubectl get pods --selector="env in (prod,test,dev)"
  kubectl get pods --selector="env in (prod,test,dev)" --show-labels
  kubectl get pods --selector="env notin (prod,dev)" --show-labels
  kubectl get pods --selector="app!=nginx" --show-labels
  ```
* Lets create labels in the declarative approach
  ```
  apiVersion: v1
  kind: Pod
  metadata:
    name: labelsdemo
    labels:
      env: dev
      app: qtweb
      ver: 1.1.0
  spec:
    containers:
      - name: nginx
        image: nginx:1.21
        ports:
          - containerPort: 80
            protocol: TCP
  ```
* Selectors in the Yaml will be in the format of
  ```
  selector:
  app: web
  env: prod
  ```
* Annotations:
  Annotations are also key value pairs like labels which provide a place to store additional metadata for k8s objects with the sole purpose of assisting tools and libraries.
  ```
  metadata:
  annotations:
    qt.com/icons-url: "https://qt.com/icon-main.png"
  ```
### ReplicaSets
* ReplicaSet Manifest created in activity.yml
  ```
  apiVersion: apps/v1
  kind: ReplicaSet
  metadata:
    name: activity
  spec:
    replicas: 2
    selector:
      matchLabels:
        app: jenkins
        version: "2.334"
    template:
      metadata:
        labels:
          app: jenkins
          version: "2.334"
      spec:
        containers:
          - name: jenkins
            image: jenkins/jenkins:2.334-slim-jdk8
            ports:
              - containerPort: 8080
                protocol: TCP
  ```
* Creating replicaset
  ```
  kubectl apply -f activity.yml
  kubectl get rs -o wide
  kubectl describe rs activity
  kubectl get pods --selector="app=jenkins" --show-labels
  ```
Scaling Replicasets:
--------------------
* Manual Scaling: One way is to change the replicas in yaml file and apply the file again.
  ```
  kubectl scale replicaset activity --replicas=4 
  ```
* Auto Scaling: When we autoscale horizontal pod autoscaler (hpa) will be created
  ```
  kubectl autoscale replicaset activity --min=2 --max=5 --cpu-percent=80
  kubectl get hpa
  ```
* AutoScaling can be done by create a manifest as well
  ```
  apiVersion: autoscaling/v1
  kind: HorizontalPodAutoscaler
  metadata:
    name: activity
    labels:
      app: jenkins
      version: "2.334"
  spec:
    maxReplicas: 5
    minReplicas: 2
    targetCPUUtilizationPercentage: 80
  ```
### Namespaces
* K8s namespaces provide a mechanism for isolating a group of resources with in a single cluster.
* Name of the resources should be unique with in a namespace, but not across namespaces.
* Namespace-based scoping is applicable only for namespaced objects (Deployments, Services, Pods, Replicasets etc ) and not Cluster-wide Objects (Storage Classes, Nodes, Persistent Volumes etc).
  ```
  kubectl get namespaces
  kubectl get pods
  kubectl get pods -n kube-system
  ```
* Now we can easily create a loadbalancer using k8s object called as service. The only thing service can do is group resources /select resources based on labels and give one interface for access.
* To access the pods scaled we can use service
* Now lets create a Service manifest
  ```
  apiVersion: v1
  kind: Service
  metadata:
    name: activity6-svc
  spec:
    selector:
      app: jenkins
    type: NodePort
    ports:
      - nodePort: 32700
        targetPort: 8080
        port: 8080
        protocol: TCP
  ```
* Now if we apply the service, jenkins will be accessible on each node on port 32700 which will forward the request to service (k8s) and from there to the Pod.

### Enterprise Kubernetes Setup
* When we setup k8s for the enterprises/production environments, we would go with Highly available master nodes and then we would also create nodes
* Now we would setup the kubernetes cluster and add the nodes into the cluster
* The kubectl would be configured to run from workstations (laptops/desktops) from which deployments of applications are likely to happen.
* In CI/CD Workflow, The jenkins node or azure devops agent will be the machine where kubectl is configured. From this node we will execute the kubectl apply commands on the manifests for deploying applications.

### Kubernetes as a Service
* When we try to use Kubernetes as a Service => (AKS, EKS, GKE)
* Master nodes will be managed by the Service Provider (AWS, Azure, GCP)
* Kuberentes installations will be done by the Service Provider
* We just need to Specify the number of nodes and kubernetes version
* Service providers also offer upgrade of k8s from one version to other without downtime.
Responsibility:
---------------
* Create a k8s cluster just by specifying version and number of nodes
* Configure kubectl on the nodes from where you are expected to deploy k8s manifests.

* When we use Kubernetes as a Service, The cloud providers already have loadbalancer, The Services which we create, now can be exposed to the external world using cloud load balancer.
* In Docker/Kuberenets we need to deal with Storage i.e. in Docker we have create volumes. 
* When we use kubernetes as a Service, Cloud Service Providers make it extremly simple for us to create Storage solutions as they already have solutions for creating
* virtual disks for Virtual Machines
* virtual file Share (NFS) to share storage across VMs.

### Create AKS cluster
* Create an AKS cluster with the "--enable-addons monitoring" and "--enable-msi-auth-for-monitoring" parameter to enable Azure Monitor Container insights with managed identity authentication.
* Lets create a resource group & create a k8s cluster with 2 nodes
  ```
  az group create --name myResourceGroup --location eastus
  az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 2 --enable-addons monitoring --generate-ssh-keys
  ```
* Connect to the cluster
  * Install kubectl locally
  ```
  az aks install-cli
  ```
  * Configure kubectl to connect to your Kubernetes cluster
    * Downloads credentials and configures the Kubernetes CLI to use them.
    * Uses ~/.kube/config, the default location for the Kubernetes configuration file. Specify a different location for your Kubernetes configuration file using --file argument.
    ```
    az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
    ```
* Verify the connection to your cluster
  ```
  kubectl get nodes
  ```

### Deployments
* When we deploy some application on k8s and there is no next release of this application, then using replicaset is the best option.
* But, we will have new releases to the application every day, every week etc… We need to have an option to deploy the new version of the application without having an impact on the customer/users
* In k8s we have Deployment object exists to manage the release of new versions.
* Deployments enables us to easily move from one version to another => rollout
* Deployments can roll out a new version without down time and if the new version is not performing as expected, we can roll back (undo rollout) to the older version
* Deployments manage replica sets, which in turn manages the Pods and replicas
* Creating a deployment of a sample application. Create a deployment test.yml using manifest
  ```
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: testapp-deploy
  spec:
    replicas: 2
    selector:
      matchLabels:
        app: testapp
        ver: 1.0.0
    template: 
      metadata:
        labels:
          app: testapp
          ver: 1.0.0
      spec:
        containers:
          - name: testapp
            image: shaikkhajaibrahim/testapp:1.0.0 ##Create a sample application using Docker through dockerfile and push it to the dockerhub account and use it as a image for deployment
            ports:
              - containerPort: 80
                protocol: TCP
  ```
  ```
  kubectl apply -f test.yml
  kubectl get deploy
  kubectl get deploy -o wide
  kubectl describe deploy testapp-deploy
  ```
### Service
* Service is an abstraction which defines a logical set of Pods and a policy by which to access them.
* Create the service manifest
  ```
  apiVersion: v1
  kind: Service
  metadata:
    name: testapp-svc
    labels:
      app: test
  spec:
    selector:
      app: test
    type: LoadBalancer
    ports:
      - port:80
        protocol: TCP
        targetPort: 80
  ```
* Creating service
  ```
  kubectl apply -f testapp-svc.yml
  kubectl get svc -w
  ```
* More info about our deployment:
  * A rolling deployment is a deployment strategy that slowly replaces previous versions of an application with new versions of an application by completely replacing the infrastructure on which the application is running.
  ```
  kubectl rollout status deployments/testapp-deploy
  kubectl get rs
  kubectl rollout history deployments/testapp-deploy
  ```
* To have change-cause in rollout history we use annotate
  ```
  kubectl annotate deployments/testapp-deploy kubernetes.io/change-cause="first version deployed"
  ```
* Now lets try to roll back to the previous revision
  ```
  kubectl rollout undo deployments/testapp-deploy --to-revision=2
  kubectl rollout status deployments/testapp-deploy
  kubectl rollout history deployments/testapp-deploy
  ```
### Deployment Strategies
* When it comes to changing the version of the software (i.e. your application), a K8s deployment supports two strategies
  * Recreate
  * RollingUpdate

Recreate Strategy:
------------------
* This strategy updates the replica set and terminates all of the Pods associated with deployment.
* The ReplicaSet noticias that it no longer has any replicase and re-creates all the Pods using new Image.
* Once the Pods are recreated, they are running the new version.
* While this strategy is simple and fast, it has one major drawback, it leads to certain downtime of your application.

RollingUpdate Strategy:
-----------------------
* This strategy is generally preferable strategy for any user facing service.
* While it is slower than Recreate, the Rolling Update can rollout a new version of your service while it serving usertraffic, without having any downtime.
* It first creates a new Pod, then deletes an old Pod, and creates another new one. 
* It does not kill old Pods until a sufficient number of new Pods have come up, and does not create new Pods until a sufficient number of old Pods have been killed. 
* It makes sure that at least 3 Pods are available and that at max 4 Pods in total are available. 
* In case of a Deployment with 4 replicas, the number of Pods would be between 3 and 5.(*When you updated the Deployment, it created a new ReplicaSet and scaled it up to 1 and waited for it to come up. Then it scaled down the old ReplicaSet to 2 and scaled up the new ReplicaSet to 2 so that at least 3 Pods were available and at most 4 Pods were created at all times*)
* Configure: There are two Parameters that can be used to tune the rolling update behavior
  * maxUnavailable:
    * this parameter sets the maximum number of Pods that can be unavailable during a rolling update
    * It can be either set to an absolute (2) or percent (25%)
  * maxSurge:
    * This parameter controls how many extra resources can be created to acheive a rollout.
    * It can be either set to an absolute (2) or percent (25%)
*Note: Kubernetes doesn't count terminating Pods when calculating the number of availableReplicas, which must be between replicas - maxUnavailable and replicas + maxSurge. As a result, you might notice that there are more Pods than expected during a rollout, and that the total resources consumed by the Deployment is more than replicas + maxSurge until the terminationGracePeriodSeconds of the terminating Pods expires.*

Rollover:
---------

### AKS
* Subscription
* Resource group
* Cluster Details
  * cluster preset configuration
  * kubernetes cluster name
  * region
  * availability zone
  * kubernetes version - 1.23.8
  * API server availability
* Primary node pool
  * Node size
  * Scale method
  * Node count range
* Node pool
* Access:
  * Local account with k8s RBAC
  * Azure AD authentication with k8s RBAC
  *  Azure AD authentication with Azure RBAC
* Networking
  * Kubenet
  * Azure CNI
* Integartion


Jobs
Config Maps
Secrets
Init Containers in Pod
Health Checks
Storage
StatefulSet


Kubernetes cluster setup:
-------------------------
* Installing docker on master & two nodes.
* Master:
  *  ssh -i "docker.pem" ubuntu@ec2-3-22-168-28.us-east-2.compute.amazonaws.com
* Node1:
  *  ssh -i "docker.pem" ubuntu@ec2-18-188-88-204.us-east-2.compute.amazonaws.com
* Node2:
  * ssh -i "docker.pem" ubuntu@ec2-3-141-104-63.us-east-2.compute.amazonaws.com
```
curl -fsSL https://get.docker.com -o get.docker.sh
sh get.docker.sh
sudo usermod -aG docker ubuntu
```
Installing kubeadm, kubelet and kubectl:
---------------------------------------
```
 sudo apt-get update
 sudo apt-get install -y apt-transport-https ca-certificates curl
 sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
 echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
 sudo apt-get update
 sudo apt-get install -y kubelet kubeadm kubectl
 sudo apt-mark hold kubelet kubeadm kubectl
```
* check the cgroup
  ```
  docker info |grep -i cgroup
  ```
* change the cgroup to systemd
  ```
  sudo vi /etc/docker/daemon.json
  # add the following
  {
  "exec-opts": ["native.cgroupdriver=systemd"]
  }
  # execute the following statements
  sudo systemctl daemon-reload
  sudo systemctl restart docker
  ```
* Master
  ```
  * vi kubeadm-config.yaml
    * kind: ClusterConfiguration
      apiVersion: kubeadm.k8s.io/v1beta3
      kubernetesVersion: v1.21.0
      ---
      kind: KubeletConfiguration
      apiVersion: kubelet.config.k8s.io/v1beta1
      cgroupDriver: systemd
  sudo -i
  vi kubeadm-config.yaml
  kubeadm init --pod-network-cidr=192.168.0.0/16
  kubeadm reset
  ```
* then copy the output
* change the cgroup in nodes also



Docker is about building individual containers while Kubernetes is about managing and orchestrating large numbers of them