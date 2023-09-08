# K8s Workshop

## Step 1 - Prerequisites
- Hypervisor installation (VMWare, Hyper-V, Qemu,...)
- Ubuntu20.04 64bit (desktop or server)
- Access internet

## Step 2 - prepare linux
open terminal and type the following commands:  
`$ sudo apt-get update`  
`$ sudo apt-get -y install ca-certificates curl gnupg`

## Step 3 - install Docker
`$ for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done`  
`$ sudo install -m 0755 -d /etc/apt/keyrings`  
`$ sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg`  
`$ sudo chmod a+r /etc/apt/keyrings/docker.gpg`
`$ echo
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" |
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`  
`$ sudo apt-get update`  
`$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`

## Step 4 - install kubectl
`$ curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"`
`$ sudo chmod +x kubectl; sudo mv kubectl /usr/local/bin`

## Step 5 - install Kind
`$ [ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64`  
`$ sudo chmod +x kind; sudo mv kind /usr/local/bin`

## Step 6 - install k8s cluster with Kind
`$ curl -LO https://raw.githubusercontent.com/dt-wv/k8s/main/workshop/kind-setup.yaml`  
`$ sudo kind create cluster --config kind-setup.yaml`  

### Verify k8s cluster
`$ sudo kubectl get nodes`

## Step 7 - install Dynatrace as CloudNativeFullStack
Link to Dynatrace [CloudNativeFullStack](https://www.dynatrace.com/support/help/setup-and-configuration/setup-on-k8s/installation/cloud-native-fullstack)

Dynakube can be downloaded [here](https://raw.githubusercontent.com/dt-wv/k8s/main/workshop/dynakube-cloudnativefullstack.yml)




