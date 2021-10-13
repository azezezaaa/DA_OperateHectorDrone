# DA_OperateHectorDrone
This repo contains the files used to operate a Hector drone. This repo was used as lab practical in MIAR.

## (1) Install prerequisites:
```
$ mkdir -p ~/hector_dave_ws/src
$ wstool init src https://raw.github.com/tu-darmstadt-ros-pkg/hector_quadrotor/kinetic-devel/tutorials.rosinstall
$ sudo apt update 
$ sudo apt install ros-melodic-gazebo-ros-control  ros-melodic-ros-control ros-melodic-geographic-info ros-melodic-joy ros-melodic-teleop-twist-keyboard
$ sudo apt-get install libqt4-dev
$ catkin_make && source devel/setup.bash
```
## Part 1
### (1) Launch the simulation for the hector drone. In one terminal, execute:
```
$ roslaunch hector_quadrotor_demo outdoor_flight_gazebo.launch
```
### (2) For teleoperation of the drone, execute the following in another terminal:
```
$ cd ~/hector_dave_ws/
$ source devel/setup.bash
$ rosservice call /enable_motors "enable: true"
$ rosrun teleop_twist_keyboard teleop_twist_keyboard.py
```
## Part 2
### (1) Pre-requisites:
```
$ cd ~/hector_dave_ws/src/
$ git clone https://github.com/azezezaaa/DA_OperateHectorDrone
$ cd ~/hector_dave_ws/src/DA_OperateHectorDrone/src/
$ chmod +x *.py
$ cd ~/hector_dave_ws/
$ catkin_make && source devel/setup.bash
```
### (2) To find the relevant topics:
Open a terminal and write: 
```
$ rostopic list | grep /cmd_vel
$ rostopic list | grep /ground_truth
```
### (3) To regulate the drone's altitude:
1. On Terminal A:
```
$ cd ~/hector_dave_ws/
$ source devel/setup.bash
$ roslaunch hector_quadrotor_demo outdoor_flight_gazebo.launch
```
2. On Terminal B:
```
$ cd ~/hector_dave_ws/
$ source devel/setup.bash
$ rosservice call /enable_motors "enable: true"
$ rosrun DA_OperateHectorDrone altitude_service.py
```
### (4) To manually modify the desired altitute on terminal B:
```
$ rosservice call /altitude_service "altitude:data:'2'"
```
## Part 3
### Make the drone rejoin a waypoint:
1. On Terminal A:
```
$ cd ~/hector_dave_ws/
$ source devel/setup.bash
$ roslaunch hector_quadrotor_demo outdoor_flight_gazebo.launch
```
2. On Terminal B:
```
$ cd ~/hector_dave_ws/
$ source devel/setup.bash
$ rosservice call /enable_motors "enable: true"
$ rosrun DA_OperateHectorDrone drone_move_service.py
```
### To modify for a new waypoint on Terminal B:
```
rosservice call /drone_move_service "altitude:data:'5' horizontal_x:data:'3' horizontal_y:data:'0'"
```
## Part 4
### Mission Planification
1. On Terminal A:
```
$ cd ~/hector_dave_ws/
$ source devel/setup.bash
$ roslaunch hector_quadrotor_demo outdoor_flight_gazebo.launch
```
2. On Terminal B:
```
$ cd ~/hector_dave_ws/
$ source devel/setup.bash
$ rosservice call /enable_motors "enable: true"
$ rosrun DA_OperateHectorDrone drone_move_service.py
```
3. On Terminal C:
```
$ cd ~/hector_dave_ws/
$ source devel/setup.bash
$ rosrun DA_OperateHectorDrone waypoints.py
```


