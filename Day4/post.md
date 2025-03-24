Link: https://www.linkedin.com/posts/sayantan-samanta_k8s-day4-pod-activity-7303270640394919936-8SUT?utm_source=share&utm_medium=member_android&rcm=ACoAADbNCaIBkFADKwDSu_dlAUDU-CfjobcEmvc

Replication Controller and Pod Management
5/3/2025 hashtag#K8s hashtag#Day4

🛠 hashtag#Pod Manifest
👉Check The image1
Defined a Pod (kind: Pod) with the name mypod5.
Added labels (app: web, region: US, team: prod) to identify and manage the pod.
Under spec, defined container details: name, image.
 
To show the defined labels.
kubectl get pods --show-labels

To filters out based on the labels given.
kubectl get pods --selector app=web


🔄 Converting the hashtag#Pod Manifest into a hashtag#ReplicationController
1️⃣ Defining API Version & Kind
The first part remains the same:
apiVersion: v1
kind: ReplicationController

2️⃣ RC Metadata Section
metadata:
 name: "myrc1"
We specify the name of the RC (myrc1), so we can manage it later using kubectl.

3️⃣ RC Spec Section
🔹 replicas – Setting the Desired Number of Pods
replicas: 1
This tells Kubernetes to always maintain one replica of the pod. If the pod crashes, Kubernetes will automatically restart it.

🔹 selector – Choosing Which Pods to Manage
selector:
 team: prod
This is critical! The RC needs a way to identify the pods it manages. The selector must match the labels inside the template.

🔹 template – Defining the Pod Specification
The template section is where we define the pod that the RC will create and manage.
❗The content is mostly same as Pod Manifest.

First, we define metadata for the pod inside the template:
metadata:
 labels:
 app: web
 region: US
 team: prod
These labels must match the selector (team: prod) so the RC knows which pods belong to it.

Then, we define the pod spec, which is the same as the standalone pod manifest:
spec:
 containers:
 - name: "myc1"
 image: "vimal13/apache-webserver-php"

🚀 Now, how does the hashtag#RC work? 
If one copy of the pod is already running, it will recognize it and map it. But if a pod goes down, the RC will immediately detect it and launch a new pod using the template details we provided.

We can check this by using kubectl describe rc <RC-name>. 

This will show the events and confirm if a new pod was launched. The RC will always create new pods with the same labels and specifications.

📌Scaling Replicas
There are two ways to scale the number of replicas:
1. Offline way – Modify the manifest file, change the `replicas` count, and apply it again using `kubectl apply -f <file-name>`.

2. Online way (on-the-fly scaling) – Use the command:
 kubectl scale rc <RC-name> --replicas=<desired-count>

📌hashtag#RuntimeYAML vs. hashtag#OfflineYAML
The manifest file we create is stored on our local system, but Kubernetes also manages a runtime YAML version for every resource. This is the actual YAML configuration running inside the cluster.
To retrieve and edit the runtime YAML, use:

# kubectl edit rc <RC-name>

This opens the YAML file for the running resource, allowing you to make live changes. If you modify the replica count here and save, Kubernetes will apply the changes immediately.

Vimal Daga LinuxWorld Informatics Pvt Ltd
hashtag#DevOps hashtag#DevOps_with_Vimal_Daga hashtag#SRE
