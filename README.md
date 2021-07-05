# arduino_robot_arm
Download ROS and run the robotic arm on Rviz and Gazebo

# In this repository, we will go through these steps to download ROS and run the robotic arm on Rviz and Gazebo:
Before installing ROS we need to download VMware and Ubuntu 18.04:
## 1.	Download VMware via: https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html
 After downloading VMware you need to activate the program by typing this serial number: 
ZF3R0-FHED2-M80TY-8QYGC-NPKYF
## 2.	Download Ubuntu 18.04 desktop image via: https://releases.ubuntu.com/18.04/

# •	Install ROS "melodic":
Open the terminal and type these commands:

$	sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
$	sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654 
$	sudo apt update
$	sudo apt install ros-melodic-desktop-full
$	apt search ros-melodic
$	echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
$	sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
$	sudo apt install python-rosdep
$	sudo rosdep init
$	rosdep update

To start the ROS (master node)
$	roscore

# •	Preparing ROS:

$	source /opt/ros/melodic/setup.bash
Creating a workspace by using catkin_make:
$	mkdir -p ~/catkin_ws/src
$	cd ~/catkin_ws/
$	catkin_make
$	echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
$	source ~/.bashrc

# •	Installing the package arduino_robot_arm:
Add the "arduino_robot_arm" package to "src" folder:
$	cd ~/catkin_ws/src
$	sudo apt install git
$	git clone https://github.com/smart-methods/arduino_robot_arm.git
Install all the dependencies:
$	cd ~/catkin_ws
$	rosdep install --from-paths src --ignore-src -r -y
$	sudo apt-get install ros-melodic-moveit
$	sudo apt-get install ros-melodic-joint-state-publisher ros-melodic-joint-state-publisher-gui
$	sudo apt-get install ros-melodic-gazebo-ros-control joint-state-publisher
$	sudo apt-get install ros-melodic-ros-controllers ros-melodic-ros-control
$	sudo nano ~/.bashrc
At the end of the (bashrc) file add the follwing line: 
(source /home/(your Ubuntu OS name) /catkin_ws/devel/setup.bash)
Then press in order:
ctrl + o (to write out)
ENTER
Ctrl + x (to exit)

Compile the package using:
$	catkin_make
To run Rviz use this command:
$	roslaunch robot_arm_pkg check_motors.launch

# •	Using Arduino with ROS:
Download Arduino IDE (linux version) Inside the Ubuntu via: https://www.arduino.cc/en/Main/Software

Install rosserial using:
$	sudo apt-get install ros-melodic-rosserial-arduino
$	sudo apt-get install ros-melodic-rosserial

Install ros_lib into the Arduino Environment using:
$	cd <Arduino>/libraries
$	rm -rf ros_lib
$	rosrun rosserial_arduino make_libraries.py .
Controlling the motors in simulation:
$	roslaunch robot_arm_pkg check_motors.launch
$	roslaunch robot_arm_pkg check_motors_gazebo.launch
$	rosrun robot_arm_pkg joint_states_to_gazebo.py
You may need to change the permission: 
$	cd catkin/src/arduino_robot_arm/robot_arm_pkg/scripts
$	sudo chmod +x joint_states_to_gazebo.py
Creating the manipulation by using MoveIt:
$	roslaunch moveit_setup_assistant setup_assistant.launch
To run MoveIt (Rviz):
$	roslaunch moveit_pkg demo.launch
To run MoveIt (with Gazebo):
$	roslaunch moveit_pkg demo_gazebo.launch


