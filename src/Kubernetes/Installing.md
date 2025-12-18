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

The Software Requirements for installing minikube in linux is:
- Linux (Ubuntu, Debian, Fedora, Arch, etc.)
- 64-bit architecture (x86_64 / amd64)

## Container or Driver:
- Minikube needs a driver to run Kubernetes. You must install at least one of the following:
- podman
- Docker
- KVM2
- virtual box

## Installing Container:
# Docker(recommended for beginners):
- Docker is the most widely used container runtime and is recommended for beginners.

Step 1: Install Required Dependencies
- sudo apt install -y ca-certificates curl gnupg lsb-release
Step 2: Add Docker’s Official GPG Key
- sudo mkdir -p /etc/apt/keyrings
- curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/ap
Step 4: Add Docker Repository
- echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
Step 5: Install Docker Engine
- sudo apt update
- sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
Step 6: Start and Enable Docker
- sudo systemctl start docker
- sudo systemctl enable docker
Step 7: Verify Docker Installation
- docker --version


# Podman
- Podman is a daemonless, rootless container engine and is Kubernetes-compatible.

Step 1: Update System Packages
- sudo apt update
Step 2: Install Podman
- sudo apt install -y podman
Step 3: Verify Podman Installation
- podman --version

## Installing inside of desktop environment

You can directly download the binary and move it to /usr/local/bin to run it from anywhere in the system.

```bash
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
```
You can find other installation steps [here](https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download)
