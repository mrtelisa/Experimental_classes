# Experimental Laboratory Classes

- This repo contains the package `erl1`

- When it comes to the simulation with the MOGI robot, it is necessary to have also the package you find at the following link: `https://github.com/CarmineD8/erl1_sensors`

- The folder `meshes` il cloned from `https://github.com/CarmineD8/meshes`

- When gps is integrated, to see the robot moving you can run the command
`python3 gps_follower.py` in the folder `erl1_sensors`, obtained by cloning the repo previously linked

- When `lidar` is added, you need to subscribe (in the file spawn_robot.launch.py) to the bridge of the erl1_sensors pkg this two topics:
`"/scan@sensor_msgs/msg/LaserScan@gz.msgs.LaserScan",`
`"/scan/points@sensor_msgs/msg/PointCloud2@gz.msgs.PointCloudPacked",`

- When substituting the camera with a rgbd one, you need to remove the subscription (in the file spawn_robot.launch.py) to the bridge of the erl1_sensors pkg this two topics:
`"/camera/image@sensor_msgs/msg/Image@gz.msgs.Image",`
`"/camera/camera_info@sensor_msgs/msg/CameraInfo@gz.msgs.CameraInfo",`
and then add these two new ones:
`"/camera/depth_image@sensor_msgs/msg/Image@gz.msgs.Image",`
`"/camera/points@sensor_msgs/msg/PointCloud2@gz.msgs.PointCloudPacked",`