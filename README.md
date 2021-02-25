# Google-Cartographer-with-Velodyne16

This repository is for demostrating SLAM using Velodyne 16 Lidar, with Google Cartographer SLAM package in ROS environment. 
 
 (Google Cartographer SLAM:  https://google-cartographer-ros.readthedocs.io/en/latest/ )
 
 (ROS Robot Operating System: http://wiki.ros.org/kinetic  )

video demo on Youtube: https://www.youtube.com/watch?v=XRpibHqHsPU

This Lidar is equiped with 16 channels of laser, thus produces 16 rings of signals at 10 hertz for localization and mapping. 
IMU provides 3-axis acceleration and 3-axis gryoscope, with convariance matrices. 

To use these files on your robot, you could create your own ros package in catkin_ws or simply move these files into corresponding location in the installed Cartographer_ros package. 
Remember to modify the link names of lidar, IMU, base_link and etc. 

If everything is set correctly, using roslaunch to start the sensors and cartographer_launch_file, and RVIZ will automatically open. 

Some tips for setting up the config files are listed below, and some my experience.

========================================================================

For point cloud, it could be either 2D or 3D.
2D point cloud can only produce 2D SLAM, while 3D point cloud can produce either 2D or 3D SLAM.
If you use some 2D Lidar, like RPLidar, remember to change frame names, and rostopic names.
Velodyne Lidar package provides both 3D and 2D point cloud.

According to Google Cartographer webpages, 2D SLAM can run without IMU, but, from my experience, the performance is not good, you could easily lost while moving fast. 

========================================================================

tf and frames:

Some links might be helpful for debugging tf: 

Cartographer config lua settings:
https://google-cartographer-ros.readthedocs.io/en/latest/configuration.html

Cartographer Ros API:
https://google-cartographer-ros.readthedocs.io/en/latest/ros_api.html#cartographer-node

Confusion about TF frames used:
https://github.com/cartographer-project/cartographer_ros/issues/300

Odometry with Cartographer:
https://answers.ros.org/question/311263/odometry-with-cartographer/

there can be only exact one source of odometry in this slam system, either generated from Cartographer, or generated from other sensors (e.g. wheel encoders).

if using other sensors, then 
  provide_odom_frame = false,
  use_odometry = true,
  tracking_frame = "imu_link",
  published_frame = "odom",
  odom_frame = "odom",

  and your tf tree, before running cartographer, should be like:
    odom -> base_link -> { imu_link / lidar_link / other_accessory}
  cartographer will build the transform:   map -> odom


if using cartographer odometry, then
  provide_odom_frame = true,
  use_odometry = false,
  tracking_frame = "imu_link",
  published_frame = "base_link",
  odom_frame = "odom",

map frame is always 'map', unless you have 'odom' already attached to another link 'xxx', then map frame might be 'xxx' in this case.(I have not tested this kind of setup)

========================================================================

You could use the absolute path of lua/urdf files in launch file. This could be helpful because there are multiple cartographer_ros locations.  

========================================================================

If map -> odom transform acts stable but weird orientation, then check imu reading and orientation. Cartographer seems to build map->odom transform based on imu readings. 










