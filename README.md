# NR-LOAM
This repository shares the dataset of our publication "NR-LOM: LiDAR Odometry and Mapping Integrating 5G New Radio Technology"
The raw data includes LiDAR, IMU, GNSS, encoder measurements in rosbag. Besides we also provide raw 5G measurements and real-time 5G positions from 5G PRU. You can compute the 5G positions yourslef with provided 5G base station localization info (in local coordinates and WGS84) or use the real-time positions. Please notice the real-time positions are not accurate enough with many outliers, and we suggest applying a filter with internal IMU data to smooth the trajectory. 
Then you can simply merge the 5g positions with rosbag, as the 5G PRU is already syncnized with our IMU and LiDAR, you can merge them with python script.
