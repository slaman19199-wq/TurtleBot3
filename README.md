# TurtleBot3
إعداد وتشغيل TurtleBot3 على ROS2 Humble
 طريقة إعداد وتشغيل روبوت TurtleBot3 باستخدام ROS2 Humble، مع بيئة المحاكاة Gazebo، ونظام رسم الخرائط Cartographer، بالإضافة إلى حزمة Navigation2 للتنقل الذاتي.

⸻

 الخطوة 1: تثبيت الحزم الأساسية

أول شيء قمت بتثبيت جميع الحزم الخاصة بالمحاكاة ورسم الخرائط والملاحة باستخدام الأوامر التالية
sudo apt install ros-humble-gazebo-*
sudo apt install ros-humble-cartographer
sudo apt install ros-humble-cartographer-ros
sudo apt install ros-humble-navigation2
sudo apt install ros-humble-nav2-bringup
 الخطوة 2: إنشاء مساحة العمل
source /opt/ros/humble/setup.bash
mkdir -p ~/turtlebot3_ws/src
cd ~/turtlebot3_ws/src/
 
⸻

 الخطوة 3: تحميل حزم TurtleBot3
git clone -b humble https://github.com/ROBOTIS-GIT/DynamixelSDK.git
git clone -b humble https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
git clone -b humble https://github.com/ROBOTIS-GIT/turtlebot3.git
 الخطوة 4: بناء المشروع
sudo apt install python3-colcon-common-extensions
cd ~/turtlebot3_ws
colcon build --symlink-install
ثم أضفت مسار التثبيت إلى ملف الـ .bashrc حتى يتم تحميل الإعدادات تلقائيًا في كل مرة أفتح فيها الطرفية
echo 'source ~/turtlebot3_ws/install/setup.bash' >> ~/.bashrc
source ~/.bashrc

 الخطوة 5: تشغيل المحاكاة في Gazebo
export TURTLEBOT3_MODEL=burger
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
الخطوة 6: تشغيل رسم الخرائط (Cartographer
export TURTLEBOT3_MODEL=burger
ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True
 الخطوة 7: التحكم في الروبوت
export TURTLEBOT3_MODEL=burger
ros2 run turtlebot3_teleop teleop_keyboard
 الخطوة 8: حفظ الخريطة
ros2 run nav2_map_server map_saver_cli -f ~/map
 النتيجة النهائية

بهذه الخطوات تمكنت من تشغيل TurtleBot3 في بيئة Gazebo، والتحكم به يدويًا، وإنشاء خريطة باستخدام Cartographer، تمهيدًا لاستخدامها لاحقًا في التنقل الذاتي بواسطة Navigation2
