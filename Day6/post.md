Link: https://www.linkedin.com/posts/sayantan-samanta_k8s-day6-kubernetes-activity-7307966570931085312-_3JC/?utm_source=share&utm_medium=member_android&rcm=ACoAADbNCaIBkFADKwDSu_dlAUDU-CfjobcEmvc

𝐊𝐮𝐛𝐞𝐫𝐧𝐞𝐭𝐞𝐬 𝐍𝐨𝐝𝐞𝐏𝐨𝐫𝐭 𝐒𝐞𝐫𝐯𝐢𝐜𝐞 𝐚𝐧𝐝 𝐑𝐞𝐩𝐥𝐢𝐜𝐚𝐒𝐞𝐭 
18/3/2025 hashtag#K8s hashtag#Day6

hashtag#Kubernetes Pod Connectivity
- Each hashtag#pod in Kubernetes gets a unique internal IP.
- Pods within a cluster can communicate as they share the same network.
- External users cannot directly access pods as they are private by default.

⏭Test
➞kubectl exec -it pods/<pod1> -- bash
➞ping <pod2_ip>

hashtag#Services
-Stable Access: Pods are ephemeral, and their IPs change over time.
- External Exposure: Services enable external access while maintaining security.
- hashtag#LoadBalancing: Services distribute traffic across multiple pods.

hashtag#PublicServices (hashtag#ReverseProxy Concept)
- Users send requests to a Service, not directly to a pod.
- The Service forwards the request to an available pod and retrieves the response.
- This ensures stable connectivity and built-in load balancing.

hashtag#ClusterIP: Internal Communication
- Default service type, accessible only within the cluster.
- Used for internal components like databases.

hashtag#NodePort
- Requests flow as:
 1. User sends a request to `NodeIP:NodePort`.
 2. kube-proxy take the request and forwards it to the appropriate service.
 3. The service routes it to an available pod.
 4. The response is sent back through the same path.

NodePort Components
1. Target Port - Port where the application runs inside the pod.
2. Port - Port exposed on K8s Service. (Service Port)
3. NodePort - Static port on each node for external access.

Creating a NodePort Service
kubectl expose pod <pod-name> --type=NodePort --port=1234 --target-port=80

Kubernetes assigns a NodePort (default range: 30000-32767).
- Access the service using `http://<NodeIP>:<NodePort>`.

Service-to-Pod Mapping with Labels and Selectors
- Pods have labels (e.g., `app=web`).
- Services use selectors to find matching pods.
- Matching pods are registered as backends for load balancing.

Exposing a pods created by ReplicaSet
➞ kubectl expose rs <replica-set-name> --type=NodePort --target-port=80 --port=1234 --selector key1=value1,key2=value2,.......

⚠Svc does not understand matchExpressions format, so when ReplicaSet provides the info to control the pods to Svc in this format, it fails.
Even though, Svc understands matchLabels format in Selector.

👉Provide --selector key1=value1,key2=value2 explicitly while exposing the ReplicaSet.

➞Key Takeaways
- Services expose applications securely while providing stable access and load balancing.
- Three key ports in Kubernetes Services:
 - Target Port (inside the container).
 - Service Port (used by the Kubernetes Service internally).
 - NodePort (externally accessible port).
- Services dynamically update their backend pod list when new matching pods are created or old ones are deleted.

Vimal Daga LinuxWorld Informatics Pvt Ltd
hashtag#DevOps hashtag#DevOps_with_Vimal_Daga
