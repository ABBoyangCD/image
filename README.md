# INSTALL
## Main Scripts
* **mask_rcnn.py**  MaskRCNN takes in an image, outputs masks, boxes, labels and segmented image.
* **ur5_commander.py**  After receiving the PoseStamped message, the robotic arm moves to the specified position and performs the grasping task
* **utils.py**  Contains methods and functions that are needed for other scripts.
## Full instalation procedure
1. Install ROS Noetic:

If you have not installed ROS Noetic, please follow the URL below to do so。
```
http://wiki.ros.org/noetic/Installation/Ubuntu
```
We recommend that you install **Desktop-Full**. before installing, make sure that all your software is up to date!
```bash
sudo apt update
sudo apt upgrade
```
Input the above command in this terminal:

![Alt](https://github.com/ABBoyangCD/image/blob/main/image1.jpg)

When you input these commands and complete the update, you'll see this:

![Alt](https://github.com/ABBoyangCD/image/blob/main/image2.jpg)

This proves that you have completed the full update

2. Setup the workspace:
```bash
mkdir -p ur5_ws/src && cd ur5_ws
```
You'll see this screen:

![Alt](https://github.com/ABBoyangCD/image/blob/main/image3.jpg)

This proves that you've finished creating the workspace and are now in the workspace, so install the dependencies!。

3. Setup dependencies:
```bash
sudo apt -y install ros-noetic-moveit \
  ros-noetic-realsense2-camera \
  ros-noetic-realsense2-description \
  ros-noetic-ros-controllers
```
*Tips:
If any dependencies are missing at runtime, look up their full names and install them in the following format*
```bash
sudo apt -y install ros-noetic-<package_name>
```
An example:

![Alt](https://github.com/ABBoyangCD/image/blob/main/image4.jpg)

Since I've already done all the updates, the number 0 appears on the screen.

Continue to complete the next operation, complete the "git clone" will appear in the following screen:

![Alt](https://github.com/ABBoyangCD/image/blob/main/image5.jpg)

*The "git clone" in the above image is just an example, please do not input this command in the terminal again!*

4.  Source global ros
```bash
source /opt/ros/noetic/setup.bash
```
5. Install the robotic arm driver:
```bash
# clone the driver
git clone https://github.com/UniversalRobots/Universal_Robots_ROS_Driver.git src/Universal_Robots_ROS_Driver
```
6.  Insatll moveit calibration
```bash
# clone fork of the description. This is currently necessary, until the changes are merged upstream.
git clone -b melodic-devel-staging https://github.com/ros-industrial/universal_robot.git src/universal_robot
```
7. Install gripper driver
```bash
# get the robotiq
git clone https://github.com/jr-robotics/robotiq.git src/robotiq
```
8. Install depth camera driver
```bash
# get the camera
git clone https://github.com/IntelRealSense/realsense-ros.git src/realsense-ros
```
9. Install dependencies
```bash 
sudo apt update -qq
rosdep update
rosdep install --from-paths src --ignore-src -y --rosdistro noetic
```
10. Compile workspace
```bash 
# build the workspace
catkin_make
# activate the workspace (ie: source it)
echo "source devel/setup.bash" >> ~/.bashrc
```
After you finish "catkin_make", you will see the following screen:

![Alt](https://github.com/ABBoyangCD/image/blob/main/image6.jpg)

If you are running "catkin_make" for the first time, you will have to wait for a very long time, but eventually it will say "100%".

11. Install RealSense SDK 2.0
```bash 
#  Do not put this package into the workspace
git clone https://github.com/IntelRealSense/librealsense.git
# Follow this webpage for detailed installation:
https://dev.intelrealsense.com/docs/compiling-librealsense-for-linux-ubuntu-guide
```
12. Testing your own ROS
You can run commands to test your own ROS:
```bash 
roscore
rosrun turtlesim turtlesim_node
rosrun turtlesim turtle_teleop_key
```
*Please note, be sure to run all three commands in all three terminals!*

![Alt](https://github.com/ABBoyangCD/image/blob/main/image7.jpg)
![Alt](https://github.com/ABBoyangCD/image/blob/main/image8.jpg)
![Alt](https://github.com/ABBoyangCD/image/blob/main/image9.jpg)

In the third screen you can control the direction of the little turtle.

In the picture above, I control the turtle to go forward first, and then control it to go left.

At this point, you have completed all the installation!
