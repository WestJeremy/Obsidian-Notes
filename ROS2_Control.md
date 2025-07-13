ROS2 Control is a framework for control of hardware components
It is a lower level programming in comparison to high level ROS 2 nodes 
The bridge between the two are often called broadcasters

### Key Components
1. Hardware interfaces
	1. API for ROS2 to physical hardware
	2. often hardware interfaces need to be written for custom hardware
	3. if you are lucky these are already written
	4. 
2. Controller manager
	1. runs different "controllers" 
		1. controllers are a type of node but might not nessesarily be a classic controler
	2. loads different controllers
	3. handles lifecycles
	4. facilitates communication between controllers and hardware

3. Controllers
	1. plugins that implement control strategy
	2. send commands to actuators
	3. receive feedback from sensors
	4. interact with high level ROS2 nodes with topics, services, and actions
	5. 

4. ROS2 Nodes and Topics
	1. high level ROS
	2. Topics are subscribe-able

**Workflow**
1. intialization
	1. controller manager inits hardware interface and loads controller
2. Data transfer
	1. hardware Interfaces
		1. Sensor data read and made available to controllers
		2. executes any commands given from controllers
	2. Controllers
		1. process incomming commands from high level ROS2
		2. publish feedback to ros2 topics
	3. High level interaction
		1. custom planning nodes communicate with lower level controllers


### Data
1. Topics
	1. Topics are subscribe-able subjects 
	2. ex. position controller subscribes to joint_states topic
2. Services
	1. Controllers provide or call ROS2 services to handle synchronous operations
	2. less used for real time operations due to latency
	
3. Actions
	1. Controllers use ROS2 actions for high level goal oriented operations
	2. for tasks with start, immediate feedback, and a result
	3. ex. trajectory contoller might use actions to accept goals, feedback, and results
	
4. Shared memory
	1. Controllers and Hardware interfaces utilize shared memory
	2. how controllers primarily read
		1. sensor values
		2. write actuator commands
	3. internal to ros2 control framework
	4. low latency
	5. ex a JointStateHandle is used by controllers to read the current state of joints
	
5. Parameters
	1. Controllers can use ROS 2 params for config and runtime adjustments
	2. Think gains, limits, modes
	3. ex PID gains are set with parameters which can later be adjusted

**Typical Data Share Workflow**
1. command input
	1. high level commands sent over topics or actions
2. Controller execution
	1. controller reads sensor values and states from hardware interface using shared memory
3. Actuator Output
	1. control commands are sent to the hardware interface using shared memory
4. Feedback
	1. joint states published on topics for monitoring or logging

**Data Example: Joint trajectory controller**
Controller:
Input: subscribes to /joint_trajectory (topic or action) to receive desired trajectory
Control loop: reads joint states via shared memory computes control commands and sends to hardware
Feedback: Publishes current joint states to /joint_states


**Summary**

ROS 2 controllers primarily use **shared memory** for real-time data exchange with hardware interfaces but can also leverage:

- **Topics** for asynchronous data exchange with other nodes.
- **Services** for on-demand operations.
- **Actions** for goal-oriented tasks.
- **Parameters** for runtime configuration.

The use of shared memory ensures low-latency, deterministic communication critical for real-time control, while topics and actions facilitate integration with the broader ROS 2 ecosystem.


**Launching**
controller managers 
spawners
	controllers
		yaml
	hardware interfaces
		URDF <ros2_control>
			`<ros2_control name="robot_hardware" type="system">`
				 `<hardware>` 
					 `<plugin>`
					 `ros2_control_demo_hardware/DefaultSystemPositionOnlyHardware`
					 `</plugin>` 
				 `</hardware>` 
				 
				 `<joint name="joint1">`
					  `<state_interface name="position" />` 
					  `<command_interface name="position" />` 
				  `</joint>` 
			  `</ros2_control>`


**Controllers**

Controllers are often prebuilt. In the case of a new controller the files needed will be:


methods of controllers are
	on innit
	on configure
	on activate
		state_interfaces_ and command_interfaces_ are created from the configure
	update
	deactivate
	on cleanup
	

controller.cpp
controller.hpp

controller.launch.py

controller_congig.yaml

cmake

urdf



**Launch file Errors**
	misnamed argument
		failed to load controller

**Yaml Errors**
	partial missing definition
		fail on configure
	no controller definition
		fails on load
	- misnamed type with wrong namespace
		- fails on load

**cmake Errors**
	no shared library definition
		no c++ syntax errors detected
		- colcon build runs without errors