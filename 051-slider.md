---
title: Slider Control
parent: Gados Firmware API
has_children: false
nav_order: 1
---

# Slider Control
This parts shows how to use command line to control stm. Linga, please make sure these procedures are all integrated into the script. (Perhaps douhua process)

### Calibration (Normal/Single side)
To call the calibration service, you need to provide: slider number, move (true or false), any position (except 99 for special use), 1 (for calibration). 
Slider number 99 is a special slider number to calibrate all sliders. Example for calibrating slider 0:
```
rosservice call /move_track 0 1 0 1
``` 
Example for calibrating all sliders
```
rosservice call /move_track 99 1 0 1
``` 

### Calibration (Both side) -> Get Total Steps
To call the both side calibration service, set the position value of the service call to 99, and the other values correspondingly. 
For single axis both end calibration, use the command below and the total steps will be printed.
```
rosservice call /move_track 0 1 99 1
``` 
For all axes both end calibration, slider number needs to set to 99 and use the command below
```
rosservice call /move_track 99 1 99 1
``` 
After you obtained the total steps value, you should write them to the stmconfig.yaml file. 

### Set Speed 
To change the speed of the stm32 sliders, use the following command.
```
rosservice call /set_speed [70,70,70,70,70]
```
This sets the speed for five sliders. 