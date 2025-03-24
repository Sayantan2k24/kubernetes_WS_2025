Link: https://www.linkedin.com/posts/sayantan-samanta_devops-devopsabrwithabrvimalabrdaga-activity-7294379379546034176-4hyj/?utm_source=share&utm_medium=member_android&rcm=ACoAADbNCaIBkFADKwDSu_dlAUDU-CfjobcEmvc

Date - 9/2/2025 K8s Foundation session
App runs in a container, container crashes, no one to restart it instantly, business loss.

Give this duty to a program, continuously monitor the container, if it crashes, relaunch with the same setup.

Kubernetes (K8s): Monitor Docker Engine on Node A → if app container crashes → K8s relaunches it instantly.

If Node A (host machine) goes down. 
Use Multi-node setup → K8s detects failure → launches a new container on another node (Node B) → seamlessly reroutes traffic.

K8s (does not know how to launch containers), contacts Container Engine -> contacts Container runtime to launch container.

K8s → knows available CPU/RAM of all nodes→ auto-chooses the best node to run the container.

Single-node cluster (Minikube): learning, dev, testing.
Multi-node cluster: For production → Multiple worker nodes managed by a master node (Control Plane).
Cloud-based K8s services: AWS EKS, Azure AKS, Google GKE → Fully managed.
On-premise solutions: kubeadm, OpenShift.

K8s doesn't manage nodes or infra , it is only for container management and orchestration.

Every application has a concurrency limit. Let's assume our application can handle up to 100 concurrent clients efficiently. If a 101st client tries to connect, the application will struggle to respond

Kubernetes provides horizontal scaling, where identical (replica) instances (pods) of the application are launched dynamically to share the load.

These pods are Docker containers running inside Kubernetes.
Kubernetes ensures traffic is distributed between multiple pods to balance the load.

Scaling out → Adds replicas to handle increased load.
Scaling in → Removes excess pods to save resources.

Manual scaling → Kubernetes scale command
Auto-scaling: Kubernetes automatically scales the deployment based on CPU or memory usage using the Horizontal Pod Autoscaler (HPA).

Each pod in Kubernetes gets a dynamically assigned IP address.
If a pod is deleted and recreated, its IP address changes.
A client cannot reliably connect directly to a pod because its IP may change.

Solution → we introduce an intermediary system having a program working as reverse proxy and load balancer that:
Receives traffic from clients.
Distributes the traffic evenly among available pods. (round-robin algo)
Hides backend IPs from clients for security and flexibility.

Pods → Have private IPs (isolated & free).
Exposing every pod with a public IP is impractical and insecure.
Instead, we expose a single fixed public IP through a Kubernetes Service.

Creating a Service for Public Access
To expose an application using NodePort, we use load balancer type Nodeport.
Clients connect to the NodePort, and Kubernetes routes traffic to available pods.
Clients only need to know a single ip, ip of the load balancer.

Vimal Daga LinuxWorld Informatics Pvt Ltd
hashtag#DevOps hashtag#DevOps_with_Vimal_Daga.