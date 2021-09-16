# NR-LOM
This repository shares the dataset of our publication "NR-LOM: LiDAR Odometry and Mapping Integrating 5G New Radio Technology".  The raw data contains LiDAR, IMU, GNSS, encoder measurements in rosbag. Besides we also provide raw 5G measurements and real-time 5G positions from a 5G PRS beacon.  
## 1. Data Capture
![微信图片_20210705222156](https://user-images.githubusercontent.com/40022787/133210489-9f05314f-2729-464a-bc6b-0b87ad316790.jpg) <br>
We use a SCOUT MINI chassis as the platform, the LiDAR used is a Velodyne VLP-16 and Livox Horizon, IMU&GNSS measurements come from MTI-680G. The 5G PRS measurement is from the 5G 5G PRS beacon.
## 2. Definement
### 2.1 LiDAR/IMU/GNSS/Encoder
Two rosbags are provided,<br> 
"two_rooms.bag" (6.97GB): The UGV only stays indoors to gather 5G inforamtion. <br>
"in&outdoor.bag" (8.52GB): The UGV navigates itself indoor&outdoor<br>
```C++
/gnss                   RTK measurements 
/imu/data               IMU measurements
/livox/lidar            Livox LiDAR pointclouds
/livox/imu              Livox imu information
/velodyne_points        Velodyne VLP16 pointclouds
/filter/pose_meas       encoder measurements from chassis
/filter/velocity        linear speed measurements from IMU
```
### 2.2 5G measurements
You can compute the 5G positions yourslef with provided 5G base station localization info (in local coordinates and WGS84) or use the real-time positions. Please notice the real-time positions are not accurate enough with many outliers, and we suggest applying a filter with internal IMU data to smooth the trajectory. Then you can simply merge the 5g positions with rosbag, as the 5G PRU is already syncnized with our IMU and LiDAR, you can merge them with python script.  <br>
The coordinates of eight base stations in the self-defined indoor coordinates: (using GNSS a total station) <br>
![image](https://user-images.githubusercontent.com/40022787/133213828-c5c5c48b-090a-4ab0-8b08-09e253a4f7a7.png)<br>
The respective WGS84 coordinates: <br>
![image](https://user-images.githubusercontent.com/40022787/133213960-0e98179a-9370-4437-8c94-d049143784a8.png)<br>
#### a. 5G real-time positioning file format
![image](https://user-images.githubusercontent.com/40022787/133214714-3794f1fc-5922-4fb4-bcc9-88a18f76710e.png)<br>
```
XYZ               real-time positionings 
Power             self defined power conversion, you can transform power x to dBm using 20log(x) - 83
Dis               TDOA measurements
zone              'in' means indoor 
```  
#### b. 5G raw measurements file format
![image](https://user-images.githubusercontent.com/40022787/133215650-0c50daf5-079e-40a6-8b3f-723514dd6757.png)<br>
Each sequence contains 3 files, the two bin files are used for location computation, the csv file contains the informatin from internal IMU.<br>
Internal IMU information<br>
![image](https://user-images.githubusercontent.com/40022787/133215916-5a342e40-5c87-4cad-9336-ddbda1f4f91b.png)<br>



### 2.3 Coordinates definition
`front` means UGV heading direction, `right` means UGV right direction, `up` means straight up<br>
Velodyne VLP16    `right-front-up`<br>
Livox Horizon     `right-front-up`<br>
MTI-680G          `right-front-up`<br>
## 3. Download Link
For Chinese friends, you can simply use Baidu netdisk link below:<br>
Two zip files are included, on is the rosbag, the other is the related 5G observation file, with `UERecode1.txt` contains the real-time 5G positionings. Please notice the Horizon Lidar info is not included due to limited VIP authority. <br>
中国老铁可以直接通过下面的百度云链接下载文件：<br>
每个链接里包含两个压缩文件，其中一个是bag的压缩文件，另一个是5G观测文件的压缩文件，里面最下面有个`UERecode1.txt`文件里面是实时5G定位结果。注意一下rosbag包里面没有horizon雷达的信息，因为我百度网盘没VIP,上传不了那么大文件，而且我觉得有VLP16数据大部分人应该够了。反正有需要联系我就行。<br>
[链接：https://pan.baidu.com/s/1ISd1z68W5yMvRMoeN9nJlg 
提取码：1234](https://pan.baidu.com/s/1ISd1z68W5yMvRMoeN9nJlg)

For foreign frineds, I am still working on it, as my Google Drive space is almost full.<br>
