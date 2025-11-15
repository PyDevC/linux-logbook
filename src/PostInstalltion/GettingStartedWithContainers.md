# Getting Started With Containers

## General Introductions to Containers

We can define Containers as such sandboxes which shares resources from the HostOS and shares the same kernel to perform various tasks, while providing isolation from the HostOS.
We can run any software inside the Containers, even some people or organziations uses Containers to deploy and test their softwares.

Fedora has Podman as their default containerization solutions.

## Introduction to Podman

Podman is an opensource software for creating and running virtual machines.
Podman allows the user to run a container without root privelages which makes it more safer than the containers running with root privelages.

It has several features related to running containers, and here we are only going to discuss how to run and install stuff inside containers.

## How to setup podman

Podman comes installed with Fedora

## How to use podman

First you have to pull the container images that you want to run. This step is fairly simple if you don't have a proxy setup, else you have to find your way out to pull the container.
```bash
# podman pull <image-name>:<tag>
podman pull ubuntu:latest
```

After you have installed the image, you have to run it in interactive mode to get access to the container to setup, else it will close as soon as you start it.
```bash
# podman run -it --name <custom-name> <image-name>
podman run -it --name devenv fedora
```

## Setup Podman for special usecase

Podman needs to be setup for several usecases which involve for development and testing, arbitrary software installation, expermentation.

### General Steps to Installing Container

These steps should be followed and should only be omitted if the user knows that they are doing.
Some steps are optional and can be omitted.

- If using container for general or development tasks create a user in the container.
- Setup passwd for root and newuser differently.
- According to your wish add the privelages to newuser.
- Update and upgrade your system.

### General Steps to do when installing Ubuntu Container

These things are specific to Ubuntu

### General Steps to do when installing Fedora Container

These things are specific to Fedora Containers

- run `dnf install sudo login`
- 
### For PyTorch Development
### For Arbitrary Software Installation
### For Expermentation with Compiler Constructions
### For LLVM Development and Expermentation Environment
### For Developing and Managing Python Environment
### For General Development Environment
