# Steps of Infrastructure Setup 

## 1.Creating VM's
   Created 2 VM which contains Ubuntu20.04 as os. This instances are in e2-medium class, they have 2vCpu ,1 core and 4GB memory.
   
## 2.Setting Up the VM for Create Master Node
   Installing and configuring container runtime.

## 3.Creating Master Node in Kubemaster VM.
   Following the documentation. [link](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#installing-kubeadm-kubelet-and-kubectl)
   kubeadm, kubelet, kubectl has been installed.
   
   kubeadm init.

   export KUBECONFIG=/etc/kubernetes/admin.conf

   You must deploy a Container Network Interface (CNI) based Pod network add-on so that your Pods can communicate with each other. Cluster DNS (CoreDNS) will not start up before a network is installed.

## 4.CNI Setup
   I choose flannel to configure a layer 3 network  for Kubernetes 
   
   kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml

   [flannel](https://github.com/flannel-io/flannel/blob/master/README.md#getting-started-on-kubernetes)

## 5.Switching to Worker Machine for Creating Worker Node and Attach It to Master Node
   
   Applying steps that 2. and 3.( kubeadm join insted of kubeadm init) [link](https://v1-27.docs.kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/#join-nodes)

   Now our worker and master nodes are running and communicating each other.

   ### DevOps Case 1.a
  
## 6. Installing Helm to Master Node

   Following the steps of [helm-install](https://helm.sh/docs/intro/install/#from-the-binary-releases)
   
## 7. Install Prometheus with Helm

   [link](https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus#install-chart)
   With this chart you can create ;alertmanager, kube-state-metrics, prometheus-node-exporter, prometheus-pushgateway

   There was an error about PVC depency for prometheus server but I created it manually and attach to deployment , and fixed it.

   Create node port service and on GCP add firewallrule for nodeport, we will acces to the prometheus from browser.
   
   kubectl expose svc prometheus-server --type=NodePort --target-port=9090 --name=prometheus-server-ext  

   accesing the prometheus with external-ip:nodePort
   ### DevOps Case 1.b

## 8. Create Alerts for 3 of Metrics,

   Creating metrics way on my scenario is adding alerting_rules.yml to config map. 

   ### DevOps Case 1.c








