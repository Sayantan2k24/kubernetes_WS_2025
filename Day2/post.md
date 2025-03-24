Link: https://www.linkedin.com/posts/sayantan-samanta_kubernetes-devops-devopsabrwithabrvimalabrdaga-activity-7300371509099794432-l7wm/?utm_source=share&utm_medium=member_android&rcm=ACoAADbNCaIBkFADKwDSu_dlAUDU-CfjobcEmvc

🚀 25/2/2025 Kubernetes Day 2 
At the base, we have hardware—CPU, RAM, and storage. On top of this, we install a Linux operating system. Then, we add Docker, which acts as a stage where containers will run. Together, these three form a node.
When the IT team wants to run an application, they talk to Kubernetes, which picks up the app’s image and, using Docker, turns it into a running container.

🏗️Cluster Creation
minikube start -n <node_number> -p <profile_master_node_name>

📌 Kubernetes Container Launch Flow 
1️⃣ User (kubectl) → API Server
2️⃣ API Server → Scheduler (Finds a node)
3️⃣ Scheduler → Kubelet (on the assigned node)
4️⃣ Kubelet → Docker Engine
5️⃣ Docker Engine → Container Runtime (Pulls image & starts the container)

⚠️ What Happens If a Node Fails?
Nodes can stop working for many reasons—power failure, network issues, or OS crashes. If everything runs on a single node, a failure means the whole system goes down. This is called a Single Point of Failure (SPOF).

To prevent this, we don’t rely on just one node. Instead, Kubernetes runs multiple nodes in a cluster. If one node fails, another takes over. This is called failover, and Kubernetes does it automatically, without human intervention.

📈 Scaling Applications Easily
If traffic increases, Kubernetes adds more nodes (scaling out). When traffic decreases, it removes extra nodes (scaling in).
The kube-scheduler ensures that new containers are placed where there’s enough CPU and memory, keeping the system balanced.

🚀 Deploying an Application
Running an app on Kubernetes is simple:
kubectl create deployment my-web --image=some-image
This sends a request to Kubernetes, which finds the best node to run the app.

Need more copies of the app running? Just scale it:
kubectl scale deployment my-web --replicas=3

Kubernetes spreads these replicas across different nodes to avoid overloading any single one.

🌍 Running Kubernetes Anywhere
Kubernetes can run anywhere—AWS, Azure, on-premises, or even a private cloud. This flexibility is great for companies that need to keep sensitive data (like banking info) secure while using the cloud’s benefits.

It also has a dashboard that provides a visual way to monitor everything. If using Minikube, start it with:
minikube dashboard -p [profile-name]

🛠️ Kubelet: The Agent Program
Kubelet runs on every node (both master & worker nodes).
It acts as a middleman between Kubernetes and Docker (or other container runtimes).
It continuously monitors and ensures that assigned containers stay running.

❗Commands to keep handy while testing
kubectl cluster-info
kubectl get pods -o wide
minikube ssh -p <profile> -n <node_name> -- docker ps 
minikube ssh -p <profile> -n <node_name> -- docker images

Delete a faulty node
minikube node delete -p <profile> <faulty_node>

Add a new node
minikube node add -p <profile>

Stop Nodes
minikube stop -p <profile> 

Vimal Daga LinuxWorld Informatics Pvt Ltd
hashtag#Kubernetes hashtag#DevOps hashtag#DevOps_with_Vimal_Daga hashtag#Docker
