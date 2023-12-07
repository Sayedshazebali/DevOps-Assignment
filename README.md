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
- Also enable to start at boot so $sudo systemctl enable docker
- Now downloading mini kube from official Documentary. https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/
- first download kubectl utiliy using curl command ones its downloaded just move the kubectl to bin directory
- then we have to give excutable permission to kubeclt binaries 
- curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
- sudo mv kubectl /bin/kubectl
sudo chmod a+x /bin/kubectl
After that if we check the version $kubectl Version its gives client version. but sever is not start because we didnt start kubernete yet.
Now we are going to install minikube from offical documentary.https://minikube.sigs.k8s.io/docs/start/
First, i downloaded the minikube utily and installed it and move it to  /usr/bin/kube folder.
# one more command we have to run with this minikube is not install our local cluster
$curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
$sudo install minikube-linux-amd64 /usr/bin/minikube
$sudo apt install conntrack -y
Now to check minikube is installed or not run $minikube it will respond
![image](https://github.com/Sayedshazebali/DevOps-Assignment/assets/115386350/c1efb41f-a143-4f3a-a1a9-638f33d82a26)
 # Now we start the local minikube cluster
  $minikube start --vm-driver=none
  drive=none because we already running this in ec2
  after running this running give error that "sorry, Kubernetes 1.28.3 requires crictl to be installed in root's path" Because Kubernetes v1.24 dropped support for Dockershim, if you want to use the combination of the none driver, Kubernetes v1.24+, and the Docker container runtime you'll need to install cri-dockerd on your system,  https://github.com/Mirantis/cri-dockerd
  ![image](https://github.com/Sayedshazebali/DevOps-Assignment/assets/115386350/e07c986c-0451-4470-8c7e-93e622e55485)
# installl cri-docker
apt install git -y
git clone https://github.com/Mirantis/cri-dockerd.git
mkdir bin
VERSION=$((git describe --abbrev=0 --tags | sed -e 's/v//') || echo $(cat VERSION)-$(git log -1 --pretty='%h')) PRERELEASE=$(grep -q dev <<< "${VERSION}" && echo "pre" || echo "") REVISION=$(git log -1 --pretty='%h')
go build -ldflags="-X github.com/Mirantis/cri-dockerd/version.Version='$VERSION}' -X github.com/Mirantis/cri-dockerd/version.PreRelease='$PRERELEASE' -X github.com/Mirantis/cri-dockerd/version.BuildTime='$BUILD_DATE' -X github.com/Mirantis/cri-dockerd/version.GitCommit='$REVISION'" -o cri-dockerd
sudo apt  install golang-go 


  

