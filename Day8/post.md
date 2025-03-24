Link: https://www.linkedin.com/posts/sayantan-samanta_day8-devops-devopsabrwithabrvimalabrdaga-activity-7308575612061859840-R7bh?utm_source=share&utm_medium=member_desktop&rcm=ACoAADbNCaIBkFADKwDSu_dlAUDU-CfjobcEmvc

𝐊𝐮𝐛𝐞𝐫𝐧𝐞𝐭𝐞𝐬 𝐃𝐞𝐩𝐥𝐨𝐲𝐦𝐞𝐧𝐭𝐬 & 𝐒𝐭𝐫𝐚𝐭𝐞𝐠𝐢𝐞𝐬 𝐑𝐨𝐥𝐥𝐢𝐧𝐠𝐔𝐩𝐝𝐚𝐭𝐞 𝐚𝐧𝐝 𝐑𝐞𝐜𝐫𝐞𝐚𝐭𝐞
20/3/2025 k8s hashtag#Day8

1. Introduction to Deployments
A Deployment in Kubernetes is responsible for managing and rolling out application updates efficiently. It ensures that the correct number of replicas are running and helps in version upgrades without downtime.

2. Rollout & Release Process
Rollout: Upgrading from an old image version to a new image version.
Release: Deploying the new version of the application in production.
Example: Moving from v1 → v2 → v3 → v4, ensuring new pods run with updated images.

3. Deployment Strategies in Kubernetes
Deployment guides ReplicaSet which pods to delete and create and for this Kubernetes supports multiple deployment strategies:

A) Recreate Strategy
Process:
Delete all old pods (v1).
Launch new pods (v2).
Clients connect only after the new version is fully available.

Use Case:
Used in critical situations, such as security vulnerabilities, where you must immediately remove the old version before deploying the new one.
Causes downtime as no pods are running during the transition.

B) Rolling Update Strategy
Process:
Start with multiple replicas of the current version (v1), managed by a ReplicaSet.
Introduce new pods (v2) one by one while keeping the old version running.
Register the new pods with the Service so that traffic is evenly distributed.
Gradually replace old pods:
Launch one new pod (v2), verify its connection to the client.
Once successful, remove one old pod (v1).
Repeat until all pods run v2.

Final state: Only v2 pods remain, ensuring zero downtime.

Benefits:
Ensures continuous availability by maintaining both versions during the transition.
Traffic is balanced between old and new versions.
Safer deployment with rollback capabilities.

Managing Deployments
Defining a Rolling Update Deployment
In Deployment manifest file .spec.strategy.type put "RollingUpdate".
 
Apply the configuration using: 
kubectl apply of <file>

Monitoring the Rollout
Check rollout history: 
kubectl rollout history deploy <deploy_name>

Check rollout status: 
kubectl rollout status deploy <deploy_name>

Updating the Deployment
To update the deployment from v1 to v2:
Modify the image in the deployment manifest and apply the changes.
Alternatively, use the following command:
kubectl set image deploy/<deploy_name> <cont_name>=<image_name>

<cont_name> means the the container name in the deployment manifest pod template portion.

For Details about a specific revision:
kubectl rollout history deploy <deploy_name> --revision=<number>

Rolling Back to a Previous Version
If an issue occurs after deployment, rollback using:
kubectl rollout undo deploy <deploy_name>

This is rollback to the previous version

Vimal Daga LinuxWorld Informatics Pvt Ltd
hashtag#DevOps hashtag#DevOps_with_Vimal_Daga
