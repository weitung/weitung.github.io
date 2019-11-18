---
title: Services
parent: Gados ROS Central Control Package
has_children: false
nav_order: 3
---

# Services
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

