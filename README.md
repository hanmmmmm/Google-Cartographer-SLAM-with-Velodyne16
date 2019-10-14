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
