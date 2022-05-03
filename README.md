
In this post I have covered how to install  Install Minikube in WSL 2 with Kubectl and Helm home lab environments on WLS 2 . 

__Why Minikube?__

Because, minikube is local Kubernetes, focusing on making it easy to learn and develop for Kubernetes, so home lab environments is great  choice 

__About Helm__

Helm is a package manager for Kubernetes. It makes updates and rollback of applications more efficient and improves team collaboration.


__Assumption:__

<ins>You already have set up set up wls2 windows</ins>

steps for the implementation

1. Install Docker in WSL 2
2. Install Minikube prerequisites
3. Install Minikube
4. Install kubectl and set context to Minikube
5. Install Helm
6. Start the Minikube Kubernetes cluster

### 1. Install Docker in WSL 2

The steps to install Docker in WSL 2 include:

- Install prerequisites

```jsx
sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
```
  - ### Download and add the official Docker PGP key
 
 ```jsx
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
  - ### Add the stable channel repository
 ```jsx
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```
  - ### Update the package list

 ```jsx
sudo apt-get update -y
```
 - ### Install the latest Docker CE
 ```jsx
sudo apt-get install -y docker-ce
```
  - ### Add your user to access the Docker CLI without root user permissions

 ```jsx
sudo usermod -aG docker $USER && newgrp docker
```
Summary in one img of Install Docker in WSL 2

![Example](https://github.com/eduardo152030/install-minikube-on-wsl2/blob/main/img1.png)

### 2. Install Minikube prerequisites

* There are a couple of prerequisites that blogs around the web detail as needed for installation of Minikube in WSL. These include:
  - systemctl
  - conntrack
  - Install systemctl

To install systemctl, there is a github script you need to pull down.

 ```jsx
git clone https://github.com/DamionGans/ubuntu-wsl2-systemd-script.git
```

 ```jsx
cd ubuntu-wsl2-systemd-script/
bash ubuntu-wsl2-systemd-script.sh
```
![Example](https://github.com/eduardo152030/install-minikube-on-wsl2/blob/main/img2.png)
image of Installing systemctl for installing Minikube with WSL 2

  - ### Install Conntrack

 ```jsx
 sudo apt install -y conntrack
```
![Example](https://github.com/eduardo152030/install-minikube-on-wsl2/blob/main/img3.png)

### 3. Install Minikube

* Download the latest Minikube

 ```jsx
 curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```
*  Make it executable
 ```jsx
chmod +x ./minikube
```
* Move it to your user's executable PATH
 ```jsx
sudo mv ./minikube /usr/local/bin/
```
* Set the driver version to Docker

 ```jsx
minikube config set driver docker
```
![Example](https://github.com/eduardo152030/install-minikube-on-wsl2/blob/main/img4.png)

### 4. Install Minikube
 ```jsx
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```
![Example](https://github.com/eduardo152030/install-minikube-on-wsl2/blob/main/img5.png)

Installing kubectl for use with Minikube

  - Below is the command to set the context to Minikube:

 ```jsx
kubectl config use-context minikube
```
![Example](https://github.com/eduardo152030/install-minikube-on-wsl2/blob/main/img6.png)

### 5. Install Helm to work with Minikube

  - The process to install helm involves the following steps:

```jsx
curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get > get_helm.sh 
chmod 700 get_helm.sh 
./get_helm.sh
```
![Example](https://github.com/eduardo152030/install-minikube-on-wsl2/blob/main/img7.png)

Installing helm and initializing the helm installation

### 6. Start the Minikube Kubernetes Cluster
  - After running the command to start the minikube cluster, which is:

 ```jsx
minikube start
```

  - You can see the single cluster node running using the kubectl command:

 ```jsx
kubectl get nodes -o wide
```
![Example](https://github.com/eduardo152030/install-minikube-on-wsl2/blob/main/img8.png)
