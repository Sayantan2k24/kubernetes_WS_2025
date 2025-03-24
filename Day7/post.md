Link: https://www.linkedin.com/posts/sayantan-samanta_k8s-day7-nodeport-activity-7308328958482157568-DqMV?utm_source=share&utm_medium=member_desktop&rcm=ACoAADbNCaIBkFADKwDSu_dlAUDU-CfjobcEmvc

Kubernetes Services Nodeport, ClusterIP & Best Practices for Deploying MySQL
19/3/2025 hashtag#K8s hashtag#Day7

⏭hashtag#NodePort Service
A NodePort service exposes an application externally by opening a specific port on each node. Clients access it via <node-ip>:<node-port>.

⏭Key Components:
- targetPort: The port on which the application inside the container is running (e.g., `80`).
- port: The service port that is used within the cluster (e.g., `1234`).
- nodePort: The externally accessible port on the node (e.g., `30001`). Clients connect to this port.

⏭Notes:
- `targetPort` is static as it is defined inside the container image.
- `port` (service port) can be any value within the cluster.
- `nodePort` should be between `30000-32767` (Kubernetes' allowed range). If set outside this range (e.g., `8080`), Kubernetes will throw an error and assign a value within the allowed range.

⏭Access:
Find the node IP (minikube ip).
Access: http://<node-ip>:<node-port>.

⏭ClusterIP Service (Private Service)
A ClusterIP service enables internal communication within the cluster, inaccessible externally.

⏭Key Components:
- targetPort: Port inside the container.
- port: The service port within the cluster.
- No nodePort needed.

 📌hashtag#MySQL Image Requirements
- A hashtag#database container requires environment variables to function.
- Missing variables cause hashtag#CrashLoopBackOff hashtag#Error, even though Kubernetes reports that the pod and container have launched.

📌Debugging CrashLoopBackOff Errors
- A CrashLoopBackOff indicates that the application inside the container is failing.
- To debug:
 1. Describe the pod: `kubectl describe pod <pod-name>`
 2. Check hashtag#logs: `kubectl logs <pod-name>`
- Logs reveal errors thrown by the database application (e.g., MySQL logs indicating a missing root password).
 
📌Setting hashtag#EnvironmentVariables
a) Using Command Line
 kubectl set env rs/<rs_name> MYSQL_ROOT_PASSWORD=<password>

- However, updating the environment variables this way may not immediately take effect if the pod has already failed.

b) Using YAML Manifest
in the rs manifest file spec.template.spec.containers.env here you have to specify the key value pairs
- The `env` section accepts a list of key-value pairs.

📌Restarting Pods to Apply Changes
- Even after updating environment variables, Kubernetes may not propagate them to the existing pod.
- either delete the existing pods and recreate the pod by rs.
- or delete the rs itself and create from start

📌Best Practices:
- It is a good practice to place a Kubernetes Service in front of the database container to:
- Support future scaling of database replicas.
- Ensure load balancing and proper traffic distribution.
- Use the same target port and service port.
- Other application pods should connect to `mysql-service:3306` instead of directly accessing individual database pods.
- Using ClusterIP ensures the database remains private within the Kubernetes cluster.

Vimal Daga LinuxWorld Informatics Pvt Ltd
hashtag#DevOps hashtag#DevOps_with_Vimal_Daga hashtag#SRE
