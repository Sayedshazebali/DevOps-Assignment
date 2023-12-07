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
- Now first we have to download docker
- $sudo apt install docker -y
- check the docker status $systemctl status docker
- $systemctl start docker
- 
- 
