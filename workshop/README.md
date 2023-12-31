# K8s Workshop

## Step 1 - Prerequisites
- Hypervisor installation (VMWare, Hyper-V, Qemu,...)
- Ubuntu20.04 64bit (desktop or server)  
  - 40GB disk  
  - 8GB RAM
- Access internet
- Dynatrace tenant where you can create access tokens

## Step 2 - prepare linux
open terminal and type the following commands:  
`$ sudo apt-get update`  
`$ sudo apt-get -y install ca-certificates curl gnupg dos2unix`

## Step 3 - install [Docker](https://docs.docker.com/engine/install/ubuntu/)
Remove and cleanup unnecessary packages:  
`$ for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done`  
Create a directory for the keyrings:  
`$ sudo install -m 0755 -d /etc/apt/keyrings`  
Download the gpg file for docker and add it to the keyring:  
`$ sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg`  
Make the keyring file readable:    
`$ sudo chmod a+r /etc/apt/keyrings/docker.gpg`  
Add the docker download location to the Aptitude package manager:    
`$ echo
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" |
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`  
Update the Aptitude package manager:  
`$ sudo apt-get update`  
Add the necessary packages for docker to the system via Aptitude package manager:  
`$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`

## Step 4 - install [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)  
Download latest kubectl binary:  
`$ curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"`  
Move the kubectl binary to the /usr/local/bin directory and give it the necessary rights:  
`$ sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl`

## Step 5 - install [Kind](https://kind.sigs.k8s.io/docs/user/quick-start/)
Download kind binary:  
`$ [ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64`  
Make the kind binary executable and move it to the /usr/local/bin directory:  
`$ sudo chmod +x kind; sudo mv kind /usr/local/bin`

## Step 6 - install k8s cluster with Kind  
Download the kind-setup yaml file (spec file of the kubernetes cluster)
`$ curl -LO https://raw.githubusercontent.com/dt-wv/k8s/main/workshop/kind-setup.yaml`  
Create a local kubernetes cluster with the kind-setup file:      
`$ sudo kind create cluster --config kind-setup.yaml`  
[kind-setup.yaml](https://kind.sigs.k8s.io/docs/user/quick-start/#multi-node-clusters)

### Verify k8s cluster
`$ sudo kubectl get nodes`  
[Kubectl cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

## Step 7 - install Dynatrace as CloudNativeFullStack
`$ sudo su -`

Go to the link of the Dynatrace documentation for a [CloudNativeFullStack](https://www.dynatrace.com/support/help/setup-and-configuration/setup-on-k8s/installation/cloud-native-fullstack) installation and execute all steps until step 4  

<b>Operator token scopes:</b>  
![](img/operator_k8s_token_scopes.jpg)

<b>Data ingest token scopes:</b>  
![](img/dataingest_token_scopes.jpg)

Dynakube can be downloaded and please replace the 'apiurl' with the correct value.  
`# curl -LO https://raw.githubusercontent.com/dt-wv/k8s/main/workshop/dynakube-cloudnativefullstack.yml`     
`# kubectl apply -f dynakube-cloudnativefullstack.yml`



