Link: https://www.linkedin.com/posts/sayantan-samanta_k8s-day5-replicationcontroller-activity-7305792234396778496-_ZL8?utm_source=share&utm_medium=member_android&rcm=ACoAADbNCaIBkFADKwDSu_dlAUDU-CfjobcEmvc

ReplicationController, ReplicaSet, Selectors and Load Balancing
12/3/2025 hashtag#K8s hashtag#Day5

📌Replication Controllers & Labels
 hashtag#ReplicationController uses labels (key-value pairs) to identify pods.
Uses selectors to filter pods by labels.

📌Types of hashtag#Selectors:
➞ hashtag#EqualitybasedSelectors
➞ hashtag#SetbasedSelectors

⏭Equality-based Selectors
Uses = and != to match exact values.
⚠Implement AND but not OR

Example:
➞ kubectl get pods --selector region=US

To filter pods not in the US:
➞ kubectl get pods --selector region!=US

Multiple conditions (AND logic):
➞ kubectl get pods --selector region=US,team=prod

⏭ Set-based Selectors
Uses in and notin for multiple values.
⚠ Implement AND and OR both

➞ kubectl get pods --selector "region in (US,IN)"
Works as an OR condition inside brackets.

Example with AND logic:
➞ kubectl get pods --selector "region in (US) , team in (test,prod)"

Here, region in (US) and team in (test,prod) are combined with AND.
(test,prod) Here `,` works as OR.

📌 hashtag#ReplicationController vs. hashtag#ReplicaSet
📌ReplicationController (Legacy)
Supports only equality-based selectors.
Found under v1 API version.

📌ReplicaSet (Modern)
Supports both equality-based & set-based selectors.
Found under apps/v1 API version.

To check supported API versions:
➞ kubectl api-resources

To explore selector under ReplicaSet specification fields:
➞ kubectl explain replicaset.spec.selector

👉Key fields:
➞ matchLabels → Uses key-value pairs (equality-based).
➞ matchExpressions → Uses set-based logic (in, notin).

apiVersion: apps/v1
kind: ReplicaSet
metadata:
 name: "myrs1"
spec:
 replicas: 3
 selector:
 matchLabels:
 team: prod
 matchExpressions:
 - { key: region, operator: In, values: [US] }
 - { key: app, operator: In, values: [web] }
 template:
 metadata:
 labels:
 app: web
 region: US
 team: prod
 spec:
 containers:
 - name: "myc1"
 image: "vimal13/apache-webserver-php"

or 

Set-Based selectors can be defined this way too👉
 selector:
 matchExpressions:
 - key: region
 operator: In
 values: [US]
 - key: app
 operator: In
 values: [web] 

📌 Load Balancing with Services
Managing multiple pods is an issue.
ReplicaSet handles pod replication, but not traffic distribution.

hashtag#Service is responsible for:
➞hashtag#Exposing pods via a single IP.
➞hashtag#Loadbalancing across pods.
➞Distributing traffic using hashtag#roundrobin (by default).

You can expose the pod created by rs.
➞kubectl expose rs <rs_name> --port 80 --type <type>

--type is hashtag#CLusterIP by default

It provides an internal IP that enables communication between pods within the cluster but does not expose the service externally.

Use hashtag#minikube ssh -- curl <ip_of_service>:80 to connect the service in case you are running a minikube cluster.

Vimal Daga LinuxWorld Informatics Pvt Ltd
hashtag#VimalDaga hashtag#DevOps_with_Vimal_Daga hashtag#SRE hashtag#Devops hashtag#Kubernetes
