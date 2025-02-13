Installation Environment
1.	Update 
sudo apt update && sudo apt upgrade -y


3.	Configuring Ros Noetic
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'


5.	Configuring Ros Noetic Key
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654


7.	Installing Ros Noetic
sudo apt update
sudo apt install ros-noetic-desktop-full


9.	Initializing Rosdep
sudo apt install python3-rosdep
sudo rosdep init
rosdep update


11.	Setting ROS environment variables
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc


13.	Installing Gazebo 11
sudo apt install gazebo11 libgazebo11-dev


15.	123 Installing drone-related ros packages
sudo apt-get install ros-noetic-mavros ros-noetic-mavros-extras


17.	123 Setting up mavros geolocation data
wget https://raw.githubusercontent.com/mavlink/mavros/master/mavros/scripts/install_geographiclib_datasets.sh
chmod +x install_geographiclib_datasets.sh
sudo ./install_geographiclib_datasets.sh


19.	Download px4 dependencies
sudo apt-get install git zip qtcreator cmake build-essential genromfs ninja-build exiftool -y
sudo apt-get install python3-pip
sudo -H pip3 install --upgrade pip
sudo -H pip3 install pandas jinja2 pyserial pyyaml pyros-genmsg packaging
sudo -H pip3 install numpy toml openpyxl jsonschema


21.	Clone PX4 firmware and build
sudo apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev
sudo pip3 install future
sudo pip3 install symforce
git https://github.com/PX4/PX4-Autopilot.git --recursive
cd PX4-Autopilot
make px4_sitl_default gazebo


23.	Another compilation（maybe need to copy and open another file）
 mv "/home/szacky/Desktop/PX4-Autopilot (copy)" "/home/szacky/Desktop/PX4_Autopilot_copy"
cd /home/szacky/Desktop/PX4_Autopilot_copy
make px4_sitl gazebo-classic



Configure drone formation
13.	Launching multi-drone
Tools/simulation/gazebo-classic/sitl_multiple_run.sh -n 3


14.	Configure environment
export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:~/Desktop/PX4-Autopilot
sudo apt-get update
sudo apt-get install python3-jinja2 python3-empy python3-toml
sudo apt-get install ros-noetic-mavros ros-noetic-mavros-extras
sudo apt-get install ros-noetic-mavlink ros-noetic-tf ros-noetic-tf2-ros
sudo apt-get install ros-noetic-camera-info-manager ros-noetic-mavros-msgs ros-noetic-gazebo-ros-pkgs


16.	Initialize ROS workspace
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make


18.	Configure ros environment
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc


20.	Add the px4 path to ROS_PACKAGE_PATH (you may need to add dependencies here according to your situation)
echo "export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:~/Desktop/PX4-Autopilot" >> ~/.bashrc
source ~/.bashrc


22.	Build mavlink_sitl_gazebo package
cd ~/catkin_ws/src
git clone https://github.com/PX4/PX4-SITL_gazebo.git
cd ~/catkin_ws
catkin_make


24.	Add path
source /opt/ros/noetic/setup.bash
source ~/catkin_ws/devel/setup.bash
export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:~/Desktop/PX4-Autopilot:~/catkin_ws/src
source ~/.bashrc


26.	Launching
roslaunch px4 multi_uav_mavros_sitl.launch
rosrun px4 follower_control.py（Script written by myself）
