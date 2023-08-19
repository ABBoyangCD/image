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
![Alt](https://img-home.csdnimg.cn/images/20220524100510.png)

We recommend that you install **Desktop-Full**. before installing, make sure that all your software is up to date!
```bash
sudo apt update
```
2. Setup the workspace:
```bash
mkdir -p ur5_ws/src && cd ur5_ws
```
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
11. Install RealSense SDK 2.0
```bash 
#  Do not put this package into the workspace
git clone https://github.com/IntelRealSense/librealsense.git
# Follow this webpage for detailed installation:
https://dev.intelrealsense.com/docs/compiling-librealsense-for-linux-ubuntu-guide
```
