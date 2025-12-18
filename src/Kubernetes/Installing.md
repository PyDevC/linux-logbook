# Kuberentes Installation

## MiniKub

To make a working kubernetes cluster you need to install minikube which is allows you to run a single node cluster on your local machine.

## Requirements

The hardware requirements for installing minikub in linux is:
- 2 CPU cores or more
- 2GB Free memory
- 20GB Free Storage
- Internet Connection
- Container or VM manager

## Installing inside of desktop environment

You can directly download the binary and move it to /usr/local/bin to run it from anywhere in the system.

```bash
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
```

You can find other installation steps [here](https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download)
