---
title: Quick Start
has_children: true
nav_order: 3
---

# Quick Start

## Using the docker image
First, download the ```gados_docker_launch.sh``` file (ask Weitung for this file) and send the release name in as an argument (In this case, it's ```gados-springwater-v1.1``` for linux and ```gados-springwater-v1.1.mac``` for mac). This script will help pull the specific image from the docker hub and run it in the bash, forwarding usb devices. The command we will be using is:
```
./gados_docker_launch.sh gados-springwater-v1.1
```
This will start a bash window inside the container.

### Create More Terminal Windows
If you want to connect to an existing container. Please use the following command to enter the container:
```
docker exec -it gados-docker bash
```
## Run Tests for version 1.1
For the v 1.1 version, we are able to run extensive test on the entire system. Please run the following command before running any tests described in the [subsection](http://gados-doc.gadgethi.com.tw/032-run-tests.html). 
```
roslaunch central_control firmware.launch
```