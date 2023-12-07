##### DevOps-Assignment ####
***Kubernetes Cluster Setup:***
# Use Minikube to create a local Kubernetes cluster. Document the initiation process.
Pre-requisites 
2CPU or more
2GB of memory
I am not using a virtual machine here because we are going to create a mini kube on an AWS EC2 instance.
# 1 Launch the instance 
-Use Ubuntu-server 20.04 and I take t2 medium 2CPU and 4GB RAM.
- then I create a Key-pair for SSH login
- Then I choose Network Currently I am using Default Network with Default VPC I just enabled SSH 22  Port Number for SSH Login and take Nordpod ip default range from 32000 to 32767
- Volume I take Default 8Gb
- Then I launch Instance
- I copied the Public IP address and I used MobaXtrem for SSH login.
- updating the cluster # $sudo apt-get update -y #
- # Apply updates
$ sudo apt update -y
$ sudo apt upgrade -y 
- 
# Install Minikube dependencies
$ sudo apt install -y curl wget apt-transport-https

# Download Minikube Binary

$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
* Once the binary is downloaded, copy it to the path /usr/local/bin and set the executable permissions on it *
$ sudo install minikube-linux-amd64 /usr/local/bin/minikube

Verify the minikube version
$ minikube version
$ minikube version
minikube version: v1.30.1

# Install Kubectl utility
Kubectl is a command line utility that is used to interact with the Kubernetes cluster
$ curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl

Once kubectl is downloaded then set the executable permissions on kubectl binary and move it to the path /usr/local/bin.
$ chmod +x kubectl
$ sudo mv kubectl /usr/local/bin/

# Now verify the kubectl version
$ kubectl version -o yaml
![image](https://github.com/Sayedshazebali/DevOps-Assignment/assets/115386350/d045ca52-3160-4c00-93e3-077bc2cb6d38)



# installing Docker 
Downloading from Offical Doc.

# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
# Install the Docker packages.
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
# Verify that the Docker Engine installation is successful by running the hello-world image.
 sudo docker run hello-world

 # Start minikube
As we already stated in the beginning we would be using docker as a base for minikue, so start the minikube with the docker driver, run

$ minikube start --force
![image](https://github.com/Sayedshazebali/DevOps-Assignment/assets/115386350/ac8e5f1f-5dcd-449a-b5b5-d3d61b5348d3)

# checking the Nodes
![image](https://github.com/Sayedshazebali/DevOps-Assignment/assets/115386350/da534d89-72d0-4219-ba0b-2e197ee7cb6f)

# Initialize helm
we add the ingress-nginx Helm chart repository directly
**$helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update**
# install Nginx ingress Controller
Install the Nginx Ingress Controller using the newly added repository:
**$helm install nginx-ingress ingress-nginx/ingress-nginx**

# Verify Installation
Check if the Nginx Ingress Controller pods are running:
**$kubectl get pods --namespace default -l "app.kubernetes.io/name=ingress-nginx"**

![image](https://github.com/Sayedshazebali/DevOps-Assignment/assets/115386350/dd5fd12e-d532-4392-a2bb-8dae2b3b8298)

# Create Basic Ingress Resource







 
