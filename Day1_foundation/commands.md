### Basic Cluster & Node Information:
```sh
kubectl get nodes
kubectl describe node minikube
```

### Pod & Deployment Management:
```sh
kubectl get pods -o wide
kubectl describe pods <pod-name>
kubectl get deployment
kubectl describe deployment myweb
kubectl scale deployment/myweb --replicas=4
```

### ReplicaSet Management:
```sh
kubectl get rs --show-labels
kubectl describe rs
kubectl delete rs <replica-set-name>
```

### Exposing Services:
```sh
kubectl expose deployment myweb --type=NodePort --port 81 --target-port 80
kubectl get svc myweb
kubectl describe svc myweb
kubectl delete svc myweb
```

### Networking & Connectivity Checks:
```sh
minikube ip
minikube ssh -- ifconfig
minikube ssh -- curl <cluster-ip>:<port>
kubectl get svc
```

### Debugging & Logs:
```sh
minikube ssh -- docker ps
```

### Access
Get the node ip -- single node cluster

```
minikube ip
```
get the nodePort
```
kubectl get svc 
```

Then access from outside the cluster

```
curl <node_ip>:<nodePort>
```
### Note: 

```
kubectl expose deployment myweb --type=NodePort --port 81 
```
By this, --target-port will be auto set as 81 and client will not access using servies as the application is running on some other port that is 80.

To use different port on service
```
kubectl expose deployment myweb --type=NodePort --port 81 --target-port 80
```
To use same port on service and container
```
kubectl expose deployment myweb --type=NodePort --port 80 --target-port 80
same as
kubectl expose deployment myweb --type=NodePort --port 80
```