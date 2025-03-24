Link: https://www.linkedin.com/posts/sayantan-samanta_kubectl-code-cli-activity-7302908237694042112-IvvO?utm_source=share&utm_medium=member_android&rcm=ACoAADbNCaIBkFADKwDSu_dlAUDU-CfjobcEmvc

𝐊𝐮𝐛𝐞𝐫𝐧𝐞𝐭𝐞𝐬 𝐌𝐚𝐧𝐢𝐟𝐞𝐬𝐭, 𝐘𝐀𝐌𝐋 𝐚𝐧𝐝 𝐏𝐨𝐝 𝐁𝐚𝐬𝐢𝐜𝐬
4/3/2025 K8s Day3
hashtag#kubectl (client side cmd line tool)--> Communicates with the Kubernetes API Server.

Three ways to interact with k8s cluster
hashtag#Code (YAML files)
hashtag#CLI (hashtag#kubectl commands)
hashtag#API (Direct API requests)

A hashtag#Manifest File is a YAML file where users declare the desired state of hashtag#Kubernetes resources like hashtag#Pods, hashtag#Deployments, and hashtag#Services.

hashtag#YAML (Yet Another hashtag#Markup Language) is widely used because it is human-readable and supports key-value pairs.

hashtag#Communication
Imagine two computers, A and B:

If A wants to send information to B, they need:
Standard hashtag#keys to identify data (like name, mob, id)

name: Sayantan
mob: 1111
id: 2222

Without the key attached, Program on B cannot understand which category is represented by which data.

hashtag#Keys are predefined by the hashtag#receiver (like Kubernetes)
hashtag#Values are decided by the hashtag#sender (like users)

Syntax
Key-Value Pair:
Example: name: Sayantan

List of Items (Array):
Use hyphens:
courses:
- Docker
- Kubernetes
- Ansible

hashtag#Nested Data:
Use hashtag#indentation to represent nested data:
db:
- name: "Sayantan" 
 courses:
 - Docker
 - Kubernetes

- name: "eric"
 courses:
 - AI
 - Security

Here, db is holding multiple hashtag#Records, so use `-` at starting of each Record.
Each Record have multiple values of different category, so to specify that, they belong to the same Record, use proper indentation.

A hashtag#Pod is the smallest deployable hashtag#unit in Kubernetes. It acts as a hashtag#wrapper around hashtag#containers.

hashtag#SingleContainerPod: One container inside the Pod
hashtag#MultiContainerPod: Multiple containers inside one Pod (often for sidecar patterns)

How hashtag#Kubernetes Manages Pods
Kubernetes uses hashtag#Controllers to manage Pods automatically:
hashtag#Standalone Pod: Created using kubectl run
hashtag#Deployment: Automatically recreates Pods if they fail
hashtag#ReplicaSet: Ensures a fixed number of Pod replicas are always running

A Pod YAML file contains the following key sections:
hashtag#apiVersion: API version being used
hashtag#kind: Type of resource (Pod, Deployment, etc.)
hashtag#metadata: Information like name and labels
hashtag#spec: Specifications of the Pod (Containers, images, etc.), like what to do with the the pod.

apiVersion: v1
kind: Pod
metadata:
 name: my-pod
spec:
 containers:
 - name: nginx-container
 image: nginx

To list all supported resource types by k8s:
# kubectl api-resources

To describe how to use a resource:
# kubectl explain <Resource_type>

# kubectl explain Pod
kind <string> hashtag#singleValue
apiVersion  <string> hashtag#singleValue
metadata   <ObjectMeta> hashtag#multipleValue
spec <PodSpec> hashtag#multipleValue

You can understand what keywords holds which type of data

👉 You may see --> <Object> for metadata and spec

# kubectl explain Pod.spec
containers  <[]Object> -required- means containers is must
[] means it holds a list

# kubectl explain Pod.spec.containers
name <string> -required- means name is must

Vimal Daga LinuxWorld Informatics Pvt Ltd
hashtag#DevOps hashtag#DevOps_with_Vimal_Daga hashtag#SRE
