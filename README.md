Install weave works network plugins
kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml

Installing on EKS
EKS by default installs amazon-vpc-cni-k8s CNI. Please follow below steps to use Weave-net as CNI


delete amazon-vpc-cni-k8s daemonset by running kubectl delete ds aws-node -n kube-system command

edit instance security group to allow TCP 6783 and UDP 6783/6784 ports

restart kube-proxy pods to reconfigure iptables

Create namespace

kubectl create namsepace casestudy-ns

deploy nginx deployment.yaml
kubectl apply -f deployment.yaml

deploy nginx service.yaml
kubectl apply -f service.yaml

Check node service
curl --silent 34.219.239.128:31410  | grep title

Apply network policy

Check again

Create affinity , pod anti affinity

create pdb

kubectl apply -f pdb

test pdb

kubectl cordon nodename

kubectl drain nodename --grace-period=300 --ignore-daemonsets=true

kubectl config use-context <CONTEXT-NAME>


HPA

kubectl apply -f HPA.yaml