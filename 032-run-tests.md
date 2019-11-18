---
title: Run Tests
parent: Quick Start
has_children: true
nav_order: 2
---

# Run Tests
This project is still under development. Therefore, there are a lot of tests that we need to do before making this a product. The following are the procedures to run different tests on our machine. 

## Move the Machine with Keyboard
To move the machine with the keyboard, first you need to know which zone are you trying to control. For now, there are two zones named ```bowl_area``` and ```topping_area```. Remember to run ```firmware.launch``` before running this test. Then, run the following script:
```
rosrun central_control move_douhua_machine_relative bowl_area
```
To give commands, just enter the number of axis that you are trying to control and type t or g to increase or decrease the steps for that specific number of slider. 

## QR Code Position Test
To run this test, first, you should prepare [ar marker 1](http://wiki.ros.org/ar_track_alvar?action=AttachFile&do=view&target=markers0to8.png), print it out, enter the correct dimension of the edge of the qr code to the camera_test.launch file in centimeters. Then, make sure the camera image size is set and that the camera is calibrated. Please check out [this section](http://gados-doc.gadgethi.com.tw/032-Calibration.html) to calibrate the camera. Last, run the following commands in order after running the firmware launch file:
```
roslaunch central_control camera_test.launch
roslaunch central_control transform.launch
rosrun central_control read_qr_code_positions.py
```
If the qr code can be read, it will print out the current transform of the camera position to the global origin. 