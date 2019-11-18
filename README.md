# Gados ROS Central Control Package (springwater release)
The following documentation is updated to springwater release v1.1 on 201911. I'll go through some basic functionality of this package and explain some actions required before using this package on the actual Gados machine.   Please follow the instructions on this link to do the installation and make sure you have all the dependencies before using this package. 

## Gados Block Diagram
Please contact Weitung Chen to get access to the Gados Block diagram in miro. The image quality is not very good so it won't do much if it's attached here.

## Procedure
In this section, I will introduce you to the basic procedure flow of Gados ROS Central Control package. 

## Transform

## Topics and Services 

### Topics

### Service .srv files
* (STM32 Related) GeneralCtrl: This is for controlling STM32 IO modules, e.g. suction.
#### Request
```
int16 actiontype 	# The number of the IO numbering, check PCB schematic for more information
int16 number 		# If there are more than one controls for one action type, it can be specified here. Need to check if the firmware supports this.
bool action 		# A boolean that indicates whether you want this action to be on or off. (True or False)
```
#### Response
```
bool status
```
* (STM32 Related) MoveTrack: This is for controlling STM32 sliders calibration function and relative calibration function. (Regular absolute position controls don't use this) Please check the STM32 API in the subsequent chapters to fully understand the controls of the system.
#### Request
```
int16 slider_no 	# The numbering of the sliders
bool move 			# True for commanding move and False for stopping the slider
int32 pos 			# Set the relative steps for minor calibration in the relative calibration mode. (Check the STM32 API section for more information)
bool calibration 	# set True to enter the calibration mode, set False to use the relative movement mode. 
```
#### Response
```
bool status
bool calib_status
```
* FetchOrders: This service is called when ROS wants to obtain a new order from the server.
#### Request
```
string Request 		# A dummy request header string
string order_id		# (Optional) provide a function to fetch the information of a specific order id
string order_no		# (Optional) provide a function to fetch the information of a specific order number
```
#### Response
```
string order
string order_id
string order_no
string name
string base
string soup
string main
string food1
string food2
string food3
string special
string price 
string discounted_price
string promotion
string promotion_key
int16  priority
string status
int64  time
```
* ScoopCtrl: The generate control sequence node calls the douhua scoop service and send in the basic number of scoop that it should scoop.

## Source Files
The following are the source files in this package.
* commander.py: This is the intermediate port to transform GenerateCtrlSeqNode services into topics. It acts like a driver for STM32, very important node. It transform higher level programming into something that can be understood by firmware.
* current_save_read: This is a node that helps save the current state message from the stm32 to a txt file. Therefore, if the machine loses connection, we are able to know where the current location of the machine is. This may be helpful when we want to recover our current status after losing power.  
* broadcast_transform: This node is used for broadcasting transform. All of the transform are defined in bias.yaml and all the frames are defined in ros_param.yaml. There are two kinds of transformation. The first one is the constant transformation. For this kind of transformation, the translation dict is always just the bias because the transform of thesetwo frames won't change as the machine moves. The second type is the transform that changes based on the slider current state.
* parameter_service_call.py: This node basically reads the current states from the current_state.txt file and then serve it to the parameter server so that stm is able get this.

## Config Files
There will be two main folders for configurations specific for different areas and some global configurations.
* bowl_area (zone 1):
	** stmconfig.yaml: These configurations defines the slider parameters, sensor parameters

## STM Interaction Control API
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

## Development Notes
These are some notes for the development process.

### Generate Service Header Procedure
In a computer with ROS environment, build the package with the target srv files in it. Afterwards, use the following command to generate the entire ros_lib at a specific path.
```
rosrun rosserial_client make_libraries path_to_libraries
```
Then, copy the .h header files to eclipse workspace.

