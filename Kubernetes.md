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
    * API Server:
      * This component is Central to Kubernetes. All communications between all components goes through the kube-apiserver.
      * This component is frontend of the Kubernetes control plane.
      * This component exposes a REST API.
      * We would interact with this component using kubectl by using the YAML files, which are also referred as manifests.
    * Scheduler:
      * It watches for new work tasks and assigns them to healthy nodes in the cluster.
    * etcd:
      * etcd stores the entire configuration and the state of the cluster.
      * etcd is consistent and highly available distributed key-value store.
    * Controller manager:
      * It is responsible for maintaining desired states mentioned in the manifest.
      * It looks like single component, but with in it has
        * Node Controller: for noticing & responding when node goes down
        * Replication Controller: for maintaining the correct number of pods for every replication controller object.
        * Endpoints Controller: Populates the Endpoints object
  * Node
    * Kubelet
    * Container runtime
    * Kube proxy
    * Container
