kops create cluster \
  --name mustafa.k8s.local \
  --cloud aws \
  --zones us-east-2a,us-east-2b \
  --control-plane-count 1 \
  --control-plane-size t3.small \
  --control-plane-volume-size 30 \
  --node-count 2 \
  --node-size t3.micro \
  --node-volume-size 20 \
  --dns private

  export KOPS_STATE_STORE=s3://mustafa-project-kops-state-store-12345
  kops delete cluster --name mustafa.k8s.local --yes


  #!/bin/bash

# Install Docker
yum install -y docker
systemctl enable --now docker

# Install kubectl
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
mv kubectl /usr/local/bin/

# Install Minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
install minikube-linux-amd64 /usr/local/bin/minikube

# Install required packages
yum install -y iptables conntrack

# Start Minikube
minikube start --driver=docker --force

# Verify installation
minikube status
kubectl get nodes
kubectl version --client
