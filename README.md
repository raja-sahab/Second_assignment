# Second_Assignment_RT02

## Tasks
```
To build a robot having two main features
	controlling robot & avoid obstacles
	function of increasing/ decreasing speed
```
## Implementation
```
For this task I have used two nodes i.e drive_node & speed_node
	drive_node is used to control the robot & avoid obstacles.
	speed_node is used for the function of increasing/ decreasing speed. In addition it also has a option of reset.
```

## Flowchart
The flowchart of the program is shown below.
<br>

![FlowChart](https://user-images.githubusercontent.com/96690967/154511559-e5592a4f-8cb5-4a2a-b97f-7fc65e566cab.jpeg)

## Execution
```
roscore &
catkin_make
rosrun stage_ros stageros $(rospack find second_assignment)/world/my_world.world
rosrun second_assignment drive_node
rosrun second_assignment speed_node
```
## Nodes

***1. "drive_node" in control.cpp.***
 
	Driving stragightforward without decreasing the speed when the robot doesn't detect anything in front of it. 
	Decreasing when the robot detects something in front of it. Also, in this case, depending on the place of the wall, the robot will decide the turning direction
	Turning right when the robot is close to left wall.
	Just decreasing when the robot is close to both left and right walls.
	Turning left when the robot is close to right wall.

***2. "speed_node" in interaction.cpp***

	'i' for increasing the speed 
	'd' for increasing the speed
	'r' for resetting the postion and the speed. You can move the robot into its original place anytime.
	'f' for terminating the node itself.  

## Source Codes

This program has two source codes: control.cpp and interaction.cpp.

### 1. control.cpp including "drive_node"

```
I have used four functions in control.cpp
	main function
	sensor function
	scancallback function
	speedservice function
```

***Main function***
is used to subscribe the base scan topics and advertising the speed service
	
***Sensor function***
is used to calculate distance from its surroundings by using laser sensor

***Scancallback function***
is used to collect the distance from its surroundings then use segmentation and after that alter the linear and anngular speed on the basis of segmentation

***SpeedService function***
is used to cahnge the speed as well as reset the whole program. when user gives the reset command the ros service call related to reset position is called.

### 2. interaction.cpp including "speed_node" 

```
It has a main function which is responsible for three processes.
	to get the user input
	to store that input into the server
	to send that request to the server as a client
```

## rqt-graph
I made the folder called "second_assignment." I show you the realationships between the nodes in rqt-graph. Driving node sends the commands on the velocity to stageros node. Also, driving node can get the updated velocity based on user input from speed server node with the speed.srv.
![rqt-graph](https://user-images.githubusercontent.com/96690967/155141624-38a3e342-fd98-4d71-a9a1-ea37556beaae.png)

## Final Video

https://user-images.githubusercontent.com/96690967/165139794-8056739f-8612-4415-9f96-ba8c00c15882.mp4

## Possible Improvements
In this assignment, I set the limitation of the robot since the robot will crash against the wall when the speed is too high. With PID control, the quality of control will improve and robot will drive faster than now.
