---
title: Sources
parent: Gados ROS Central Control Package
has_children: false
nav_order: 4
---

# Sources
The following are the source files in this package.
* commander.py: This is the intermediate port to transform GenerateCtrlSeqNode services into topics. It acts like a driver for STM32, very important node. It transform higher level programming into something that can be understood by firmware.
* current_save_read: This is a node that helps save the current state message from the stm32 to a txt file. Therefore, if the machine loses connection, we are able to know where the current location of the machine is. This may be helpful when we want to recover our current status after losing power.  
* broadcast_transform: This node is used for broadcasting transform. All of the transform are defined in bias.yaml and all the frames are defined in ros_param.yaml. There are two kinds of transformation. The first one is the constant transformation. For this kind of transformation, the translation dict is always just the bias because the transform of thesetwo frames won't change as the machine moves. The second type is the transform that changes based on the slider current state.
* parameter_service_call.py: This node basically reads the current states from the current_state.txt file and then serve it to the parameter server so that stm is able get this.
