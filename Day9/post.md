Link: https://www.linkedin.com/posts/sayantan-samanta_k8s-session9-devops-activity-7308940883691773953-7VCX?utm_source=share&utm_medium=member_desktop&rcm=ACoAADbNCaIBkFADKwDSu_dlAUDU-CfjobcEmvc

𝐌𝐚𝐧𝐚𝐠𝐢𝐧𝐠 𝐒𝐞𝐜𝐫𝐞𝐭𝐬 𝐚𝐧𝐝 𝐃𝐞𝐩𝐥𝐨𝐲𝐢𝐧𝐠 𝐌𝐲𝐒𝐐𝐋 & 𝐖𝐨𝐫𝐝𝐏𝐫𝐞𝐬𝐬
21/3/2025 hashtag#k8s hashtag#Session9 

Handling Sensitive Data in Kubernetes Deployments
The Problem with Plaintext Credentials
In a Kubernetes environment, some applications—such as MySQL—require environment variables to be set for proper functioning. 

If the credentials are stored directly as plaintext in the Kubernetes manifest file, it poses a security risk.

Using Kubernetes Secrets to Secure Credentials
To address this issue, Kubernetes provides Secrets, which store sensitive data separately from the manifest file. Instead of including credentials directly, the manifest references them securely.

1.Create a Secret for Database Credentials
 kubectl create secret generic mysecretbox \
 --from-literal=u=sayantan \
 --from-literal=p=mypassword

Only Kubernetes admins or users with the appropriate permissions can view the actual values.

2.Verifying the Secret
 kubectl get secret
 kubectl describe secret mysecretbox
 kubectl get secret mysecretbox -o yaml

The `describe` command will show the secret keys but not their actual values.
The `-o yaml` flag displays base64-encoded values.

3.Decoding the Secret Values
echo bXlwYXNzd29yZA== | openssl base64 -d  Decodes 'mypassword'
echo c2F5YW50YW4= | openssl base64 -d  Decodes 'sayantan'

This step highlights whyRole-Based Access Control (RBAC) is essential to restrict secret access.

Referencing Secrets in a Manifest File
Instead of specifying plaintext credentials, reference the secret in the deployment YAML file as follows:
 - name: MYSQL_PASSWORD
 valueFrom:
 secretKeyRef:
 name: mysecretbox
 key: p

Same way use u

- `name`: The variable name inside the container.
- `valueFrom`: Specifies that the value comes from a Kubernetes secret.
- `secretKeyRef`: Defines which secret and key to use.

At runtime, Kubernetes injects the values securely.

Deploying MySQL with Secrets
1.Create the deployment
2.Expose the MySQL Deployment using ClusterIP
kubectl expose deployment mysqldb --type=ClusterIP --port=3306 --dry-run=client -o yaml
The `ClusterIP` service type allows internal communication within the cluster.

3.Append the Service Definition to the MySQL Deployment YAML
kubectl expose deployment mysqldb --type=ClusterIP --port=3306 --dry-run=client -o yaml >> mysql_deploy_secret.yml

---

Deploying WordPress with MySQL Backend

1.Create the WordPress Deployment YAML
kubectl create deployment wpapp --image=wordpress:latest --dry-run=client -o yaml > wordpress_deployment.yml

2.Expose WordPress Using NodePort
kubectl expose deployment wpapp --type=NodePort --port=80 --dry-run=client -o yaml >> wordpress_deployment.yml

4.Connecting WordPress to MySQL
 - WordPress requires the database host to connect to MySQL.
 - Instead of using an IP address (which may change), reference the MySQL Service IP, as Database Host.

Vimal Daga LinuxWorld Informatics Pvt Ltd 
hashtag#DevOps hashtag#DevOps_with_Vimal_Daga
