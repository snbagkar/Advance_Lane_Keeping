# Advance_Lane_Keeping
This is an extended version of Lane_keeping. This method utilizes Sliding window mwthod for lane keeping also there are few additional steps for image processing that will be explained below.
# Introduction
This repository contains information to run a racecar using Advance Lane keeping Algorithm in a Yellow single lane track. Lane-Keeping algorithm dictates the vehicle to detect the lanes and maintain the vehicle inside this lane seen by the sensor data. For Control, PID algorithm is implimented. Simulator is made using ROS/Gazebo. The simulation has been tested on and works well in Ubuntu 16.04 with ROS Kinetic installed.
# Requirements and Dependencies
For simulation purpose mlab-upenn/f1_10_sim is used link: https://github.com/mlab-upenn/f1_10_sim 
Clone the package into your git workspace and symlink it into the `src` in the catkin_workspace.
Following are additional dependencies used to run the simulation environment
```sh
  - sudo apt-get install ros-kinetic-ros-control 
  - sudo apt-get install ros-kinetic-gazebo-ros-control 
  - sudo apt-get install ros-kinetic-ros-controllerse
  - sudo apt-get install ros-kinetic-ackermann-msgs 
  - sudo apt-get install ros-kinetic-joy
```

### Instructions to Launch vehicle in yellow lane world 

To launch the simulator run the following command: 
```
$ roslaunch race f1_tenth.launch
```
# Teleoperating the vehicle on to the track
```sh
$ python keyboard.py
```
After the Gazebo window has opened, you can click in the terminal from which you ran the launch command and teleoperate the car.
The commands used to teleoperate the car using the keyboard are: ``` W, A, S and D```
If it doesn't not teleoperate the 1st time you press a key, press it again. 

Press ```Ctrl + c``` twice to terminate the process in the terminal.


### Vehicle Characteristics:

| Velocity       | Full Left | Straight | Full Right |
| :------------- | --------- | -------- | ---------- |
| Steering value | -0.5      | 0        | 0.5        |

While using it to test an external controller, the control commands are to be issued on the topic:

`/vesc/ackermann_cmd_mux/input/teleop`

Speed is supposed to be published on `msg.drive.speed` and steering angle is to be published on `msg.drive.steering_angle` where `msg` is an `AckermannDriveStamped` message.

If these bounds are crossed, the steering geometry distorts to unrealistic angles, hence they have to be limited in the external controller itself.

# Running the lane following algorithm
```sh
$ python test.py
```
# Image processing Pipeline 
  - Read image
  - Convert BGR image to RGB
  - Convert RGB to grayscale
  - Apply Image-thresholding 
  - Apply Image wrap and percpective transform
  - Apply sliding window on Image
  ![Image Processing](https://github.com/snbagkar/Lane_Keeping/blob/main/6230e17a-59c4-400f-a3a7-0cdacc3448bd.jpeg)  

  
# For Controller basic PID controller is used 

        angle = previousAngle + kp*error + kd*(previousError - newError)
    
        velocity = previousVelocity + kp*error + kd*(previousError - newError)


# Final output
  

