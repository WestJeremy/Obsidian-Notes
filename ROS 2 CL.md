ROS2 tutorial

Nodes that can subscribe to certain topics
In ROS nodes ~= python threads

[[ROS2_Control]]
	ROS2 Control is a framework for control of hardware components
	It is a lower level programming in comparison to high level ROS 2 nodes 
	The bridge between the two are often called broadcasters





**Directory Structure**
ros2_ws
	build
	install
	log
	src

**Launch File**
Python launch files launch nodes with their parameters.
**cmd line**
mkdir -p ~/colcon_ws/src/my_package/launch
touch ~/colcon_ws/src/my_package/launch/my_launch.py

**python**
from launch import LaunchDescription
from launch_ros.actions import Node

def generate_launch_description():
    return LaunchDescription([
        # Launch the first node with custom parameters
        Node(
            package='my_package',
            executable='node1',
            name='node1_name',
            output='screen',
            parameters=[{'param1': 'value1'}],
            remappings=[('/input_topic', '/node1_input')],
        ),
        # Launch the second node with custom parameters
        Node(
            package='my_package',
            executable='node2',
            name='node2_name',
            output='screen',
            parameters=[{'param2': 'value2'}],
            remappings=[('/input_topic', '/node2_input')],
        ),
    ])

**cmd**
ros2 launch my_package my_launch.py




**Command Line**

colcon
	"collective construction"


colcon install
	pip install -U colcon-common-extensions
	sudo apt install python3-colcon common-extensions


**____Examples_______**
https://docs.ros.org/en/jazzy/Tutorials/Beginner-Client-Libraries/Colcon-Tutorial.html

**Basic workspace**

make workspace dir
	mkdir -p ~/ros2_ws/src
	cd ~/ros2_ws

Build Project
	colcon build --symlink-install
		.
		├── build
		├── install
		├── log
		└── src
		
		4 directories, 0 files

Test for built packages
	colcon test

Add Installs to Path
	source install/setup.bash
		(Run this a lot this is usually the problem.)

Make a package
	python
		ros2 pkg create --build-type ament_python my_package
	C++ or python
		ros2 pkg create --build-type ament_cmake my_package

Add source code to package
	modify **package.xml** and **CMakeLists.txt** to list dependencies, .exe, or libs
	python
		add scripts to my_package/my_package directory
	C++
		add .cpp in src

Build package
	cd ~/colcon_ws
	 colcon build

Test package
	python
		ros2 run my_package my_python_script
	C++
		ros2 run my_package my_cpp_node

To use ROS commands
with every new file
	source /opt/ros/jazzy/setup.bash
	colcon build --symlink-install
	source install/setup.bash

	source /opt/ros/jazzy/setup.bash
	source install/setup.bash


	source /opt/ros/jazzy/setup.bash
	colcon build --cmake-args -DCMAKE_BUILD_TYPE=RelWithDebInfo
	source install/setup.bash


check for packagescolcon build
ros2 pkg list

clean cache
	colcon build --cmake-clean-cache
skip package
	colcon build --packages-skip <package_name>
debug
	colcon build --cmake-args -DCMAKE_BUILD_TYPE=RelWithDebInfo

list hardware interfaces
ros2 control list_hardware_interfaces

list nodes
ros2 node list

launch a launch file
ros2 launch quadruped_bringup real_quadruped_hardware.launch.py

list nodes and parameters
ros2 param list

get value from param
ros2 param get \node parameter_name

publish value to subscriber
`ros2 topic pub /<node_name>/command std_msgs/msg/Float64 "{data: <value>}"`
	`ros2 topic pub /can_command_controller/command std_msgs/msg/Float64 "{data: 1.23}"`
	`ros2 topic pub /can_command_controller/command std_msgs/msg/UInt8MultiArray "{data: [1, 2, 3, 4, 5, 6, 7, 8]}"`

get topic info
ros2 topic echo /joint_states


[ros2 control]