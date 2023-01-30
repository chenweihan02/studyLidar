# studyLidar
2D Lidar

lesson1:  

遍历雷达数据 

实现LIO-SAM中的特征点提取

---

lesson2: scan_to_pointcloud2 scan_match_icp

- sensor_msgs/scan和sensor_msgs/PointCloud2是激光数据的两种表现形式，之间可以通过pcl相互转换

- 这里依赖pcl_ros 以及 pcl_conversions，将scan数据转化为 PointCloud2数据

- 这里ros发布PointCloud数据时，帮我们做了pcl::PointCloud --> sensor_msgs::PointCloud2，所以这里只需要做sensor_msgs::scan --> pcl::PointCloud

- scan的数据形式类似极坐标，PointCloud的数据形式类似笛卡尔坐标

- 考虑了无效值处理、std_msgs/Header header、geometry_msgs/Point32[] points

---

lesson3: scan_match_plicp

本次实现的是帧间匹配，只是最基础的帧间坐标变换的计算．接下来，将添加以下功能来实现激光里程计．

- 位姿预测功能：根据当前的速度，来对下一时刻的位姿进行预测，作为plicp的初值
- 使用 tf2 记录位姿变换，将雷达坐标系的运动转成base_link下的运动，并进行累加
- 将累加的位姿作为里程计发布出去
  





---

作者Github: https://github.com/xiangli0608