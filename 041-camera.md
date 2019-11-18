---
title: Camera Calibration and Initialization
parent: Calibration
has_children: false
nav_order: 1
---

# Camera Calibration and Initialization
In this section, we are going to talk about camera calibration processes. In this section, we will extensively use the GUI display to 

### Use USB webcams on ROS
In this section, we will explain the ways to use USB webcams with Gados ROS. First of all, connect your usb cam to your computer and check your device name in:
```
ls /dev
```
Make sure to change the device name in the ```camera_test.launch``` file. 
Then, if it's a new camera, make sure to generate a new calibration file (camera_info) for this camera by following the calibration instruction in the following [page](http://wiki.ros.org/camera_calibration/Tutorials/MonocularCalibration). The following are some important note and the main procedures.
* First of all, run the ```camera_test.launch``` file
* Then, run the following command to start the calibration process. Make sure to measure the dimension of your grid before doing this. The following is just an example.
```
rosrun camera_calibration cameracalibrator.py --size 8x6 --square 0.026 image:=/zone1/pos_calib_cam/image_raw camera:=/zone1/pos_calib_cam
```
Caution: This will call out a gui display so make sure you are on VNC or desktop forwarding mode if you are using ssh.
* You move around the grid until the calibration button becomes available. Hit it and let it calibrate. (Caution: Just hit calibrate button ONCE. It will start calibrating, it just didn't print progress)
* Hit the commit button and it should saved it to the correct place.
