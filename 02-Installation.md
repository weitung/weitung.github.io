---
title: Installation
has_children: false
nav_order: 2
---

# Installation
To get started on Gados, many dependencies and packages are needed. However, the installation process is too complicated. Therefore, a docker image is built in this [GitHub Repository](https://github.mit.edu/weitung/docker-gados). **Only developers have access to this repository - please request on company slack to get access** The following is the installation process of docker on different platforms. 

## MAC 
Follow this link[https://docs.docker.com/docker-for-mac/install/] and install the desktop environment and you are all set.

## LINUX
The following is for the installation on ubuntu environment. This docker is built for ubuntu environment so this should be enough. (The different ways of forwarding usb devices).

### Step 1: Update Software Repositories
As usual, it’s a good idea to update the local database of software to make sure you’ve got access to the latest revisions.

Therefore, open a terminal window and type:
```
sudo apt-get update
```
Allow the operation to complete.

### Step 2: Uninstall Old Versions of Docker
Next, it’s recommended to uninstall any old Docker software before proceeding.

Use the command:
```
sudo apt-get remove docker docker-engine docker.io
```

### Step 3: Install Docker
To install Docker on Ubuntu, in the terminal window enter the command:
```
sudo apt install docker.io
```
### Step 4: Start and Automate Docker
The Docker service needs to be setup to run at startup. To do so, type in each command followed by enter:
```
sudo systemctl start docker

sudo systemctl enable docker
```

