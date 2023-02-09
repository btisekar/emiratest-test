**Steps for Cluster Creation**


**Create EKS Cluster with version 1.2.4 and 2 node Group**

Use terraform module for eks cluster creation

**Install Metric server**

kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.6.2/components.yaml

**Create Namespace casestudy-ns**

kubectl create namsepace casestudy-ns

**Deploy Nginx Deployment**

kubectl apply -f deployment.yaml

**Deploy Nginx Service**

kubectl apply -f service.yaml

**Check node service**

curl --silent ipaddr:31410  | grep title

**Install weave works network plugins**

kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml

**Delete amazon-vpc-cni-k8s Daemonset**

kubectl delete ds aws-node -n kube-system

**Apply Network Policy**

kubectl apply -f networkpolicy.yaml

**Apply HPA**

kubectl apply -f hpa.yaml

**Create Pod disruption Budget**

kubectl apply -f pdb.yaml


**Test Pod disruption Budget**

kubectl cordon nodename

kubectl drain nodename --grace-period=300 --ignore-daemonsets=true




**Notes**

We would be using an existing eks cluster for test purpose as eks cluster creation takes more than 20 minutes also the terraform code is used to explain in depth terraform design and is the way to deploy a cluster in production environemnt. We have an existing vpc which would be used

**Design Details**

We have used deployment kubernetes object with two pod replicas and created node port service expose at port 31410 as node port services are allowed only between 30000 and 65000 range

We have installed Weaveworks network agent as vpc cni aws eks plugin is not sufficent to create network policy

Also we have installed metrics server as its is needed for hpa to function
