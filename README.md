# EKS
Deploying Kubernetes in AWS EKS 

## Install EKS on local or cloud shell
### for ARM systems, set ARCH to: `arm64`, `armv6` or `armv7`
ARCH=amd64
PLATFORM=$(uname -s)_$ARCH

curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"

### (Optional) Verify checksum
curl -sL "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_checksums.txt" | grep $PLATFORM | sha256sum --check

tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz

sudo mv /tmp/eksctl /usr/local/bin

## KUBECTL Installation
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

## Create a EKS cluster using EKSCTL
### Command with spot instance
eksctl create cluster --name eks-test --node-type t3.micro --nodes 2 --managed --spot
### With on demand instances
eksctl create cluster --name eks-test --node-type t3.micro --nodes 2 --managed
