---
title: Development Note
parent: Gados Firmware API
has_children: false
nav_order: 3
---

# Development Notes
These are some notes for the development process.

### Generate Service Header Procedure
In a computer with ROS environment, build the package with the target srv files in it. Afterwards, use the following command to generate the entire ros_lib at a specific path.
```
rosrun rosserial_client make_libraries path_to_libraries
```
Then, copy the .h header files to eclipse workspace.