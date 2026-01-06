# Experimental Laboratory Classes

- This repo contains the package `erl1`

- The folder `meshes` is cloned from https://github.com/CarmineD8/meshes

- When gps is integrated, to see the robot moving you can run the command  
`python3 gps_follower.py`   
in the folder `erl1_sensors`, obtained by cloning the repo previously linked

- When `lidar` is added, you need to subscribe (in the file spawn_robot.launch.py) to the bridge of the erl1_sensors pkg this two topics:  
`"/scan@sensor_msgs/msg/LaserScan@gz.msgs.LaserScan",`
`"/scan/points@sensor_msgs/msg/PointCloud2@gz.msgs.PointCloudPacked",`  
It can be visualized in Rviz by adding the topic `/scan`, and in gazebo adding the `Visualize lidar` Tool.

- When substituting the camera with a rgbd one, you need to remove the subscription (in the file spawn_robot.launch.py) to the bridge of the erl1_sensors pkg this two topics:
`"/camera/image@sensor_msgs/msg/Image@gz.msgs.Image",`
`"/camera/camera_info@sensor_msgs/msg/CameraInfo@gz.msgs.CameraInfo",`  
and then add these two new ones:  
`"/camera/depth_image@sensor_msgs/msg/Image@gz.msgs.Image",`
`"/camera/points@sensor_msgs/msg/PointCloud2@gz.msgs.PointCloudPacked",`

- To use open_cv, the repo https://github.com/CarmineD8/my_opencv should be cloned as another pkg of the workspace.
The repo for open_cv in python is instead https://github.com/CarmineD8/my_opencv_py

- For using aruco_open_cv, I tuned back from a rgbd camera to a normal one. NB: The camera must not be wide angle!  
It is also necessary to clone this repo https://github.com/SaxionMechatronics/ros2-gazebo-aruco as a new folder at the same level of `my_ros2` workspace, and the repo https://github.com/fictionlab/ros_aruco_opencv as a pkg in `my_ros2`.  
Then, after starting the simulation   
(   `colcon build` in the workspace  
    `source install/local_setup.bashrc`  
    `ros2 launch elr1 erl1_simulation.launch.py`)  
in another terminal run  
`ros2 launch aruco_opencv aruco_tracker.launch.xml`  
In this way, in the rviz environment, when clicking `Add -> By Topic`, the option `Image` under `/debugging` should be appeared, and it will show the box with the calibration mark with an axes frame.

- When wanting to create the map, the repo https://github.com/CarmineD8/ros2_navigation must be cloned as a package in the workspace, and then, before running the launch file, run `ros2 launch ros2_navigation mapping.launch.py`. The fixed frame in rviz must be setted to `map`.  
If you also want to save the map, go into the folder in which you want to save it and run `ros2 run nav2_map_server map_saver_cli -f my_map`, where my_map is the name my map has.  
The map can be visualized by adding the `/map` topic in rviz.

- Once created a map, I can load it and use it to localize the robot in the environment. To do this, I need to launch `ros2 launch ros2_navigation localization.launch.py` and set in rviz the fixed frame as `map` (if needed relaunch the localization.launch.py).  
If wanted, I can also visualize in rviz `PoseWithCovariance` to see the localization and `ParticleCloud`. Maybe they will not work at first, but changing few parameters (or re-setting the fixed frame), they should work. Remember to set the topic of `ParticleCloud` as `/particle_cloud` and to set for both topics the `Reliability Policy` to `Best Effort`.

- When wanting to navigate in an environment, launch `erl1_simulation.launch.py`, `mapping.launch.py` and `navigate.launch.py`. Then in rviz you can add the map, the cost map (local or global) and the path (local or global). You will see that, using the `2D goal pose` tool to move around the robot, the map will be updated.

- When integrating PPDL with ROS2, the following command must be run  
`(sudo) apt install "ros-jazzy-plansys2-*"`.  
In our case, it is required also to clone the repo https://github.com/CarmineD8/plansys_interface.

- The professor has run the following commands:
```bash
ros2 run plansys_interface get_plan
ros2 run plansys_interface get_plan_and_execute
ros2 launch plansys_interface distributed.launch.py
```

- To open a new plansys2 terminal, run `ros2 run plansys2_terminal plansys2_terminal`.  
By typing `get domain`, the domain will be displayed; by typing `run`, the system will try to solve the problem. The terminal will be closed by typing `quit`.

