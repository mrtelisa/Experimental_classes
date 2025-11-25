# Experimental Laboratory Classes

- This repo contains the package `erl1`

- When it comes to the simulation with the MOGI robot, it is necessary to have also the package you find at the following link: `https://github.com/CarmineD8/erl1_sensors`

- The folder `meshes` il cloned from `https://github.com/CarmineD8/meshes`

- When gps is integrated, to see the robot moving you can run the command  
`python3 gps_follower.py`   
in the folder `erl1_sensors`, obtained by cloning the repo previously linked

- When `lidar` is added, you need to subscribe (in the file spawn_robot.launch.py) to the bridge of the erl1_sensors pkg this two topics:  
`"/scan@sensor_msgs/msg/LaserScan@gz.msgs.LaserScan",`
`"/scan/points@sensor_msgs/msg/PointCloud2@gz.msgs.PointCloudPacked",`

- When substituting the camera with a rgbd one, you need to remove the subscription (in the file spawn_robot.launch.py) to the bridge of the erl1_sensors pkg this two topics:
`"/camera/image@sensor_msgs/msg/Image@gz.msgs.Image",`
`"/camera/camera_info@sensor_msgs/msg/CameraInfo@gz.msgs.CameraInfo",`  
and then add these two new ones:  
`"/camera/depth_image@sensor_msgs/msg/Image@gz.msgs.Image",`
`"/camera/points@sensor_msgs/msg/PointCloud2@gz.msgs.PointCloudPacked",`

- To use open_cv, the repo `https://github.com/CarmineD8/my_opencv` should be cloned as another pkg of the workspace.
The repo for open_cv in python is instead `https://github.com/CarmineD8/my_opencv_py`

- For using aruco_open_cv, I tuned back from a rgbd camera to a normal one. NB: The camera must not be wide angle!  
It is also necessary to clone this repo `https://github.com/SaxionMechatronics/ros2-gazebo-aruco` as a new folder at the same level of `my_ros2` workspace, and the repo `https://github.com/fictionlab/ros_aruco_opencv` as a pkg in `my_ros2`.  
Then, after starting the simulation   
(   `colcon build` in the workspace  
    `source install/local_setup.bashrc`  
    `ros2 launch bme_gazebo_sensors spawn_robot.launch.py`)  
in another terminal run  
`ros2 launch aruco_opencv aruco_tracker.launch.xml`  
In this way, in the rviz environment, when clicking `Add -> By Topic`, the option `Image` under `/debugging` should be appeared, and it will show the box with the calibration mark with an axes frame.