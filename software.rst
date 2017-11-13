Software
========

  Setting up the software for the WidowX Robot Arm isn't complicated. You will need the Arduino IDE to install firmware on to the ArbotiX-M. If you are setting up ROS, you will need a computer compatible with Xenial (Ubuntu 16.04), and ROS Kinetic.

  .. raw:: html
     :file: inclusion.html


Arduino IDE Setup
-----------------

.. raw:: html
   :url: http://www.trossenrobotics.com/Shared/readthedocs/arduinoIDEarbotix.html

Firmware
--------

  Firmware for the WidowX is dependent on how you intend to control it. For an ROS installation or to use DynaManager, you will use the ros sketch in the ArbotiX Sketches folder you downloaded in the Arduino IDE Setup. To use the Arm with the Armlink Software, you will use the Armlink Sketch and follow the Armlink instructions.


Firmware: WidowxArmTest
^^^^^^^^^^^^^^^^^^^^^^^

  A great piece of code to run for testing your WidowX Arm build is the WidowxArmTest, included in the files you downloaded in the Arduino IDE Setup. Once the program is loaded, make sure that your robot is powered from a 12v power supply, and that the power jumper is set to 'VIN'. Once the robot is programmed and powered, it will move to a 'Center Position' where each servo horn is at its centered position. You will need to wait for *~10 seconds* as the robot starts the build check. The robot should move in the exact way as shown in this video.

.. raw:: html
   :url: http://www.trossenrobotics.com/Shared/readthedocs/widowx/widowxbuildcheck.html



Firmware: ROS
^^^^^^^^^^^^^

  For an ROS install, you use the ROS sketch you downloaded in the Arduino IDE Setup. This firmware acts as a passthrough, compatible with the 'arbotix_python<http://wiki.ros.org/arbotix_python>'_ library and any derivatives. All of the configuration is handled by the software passing commands to and reading data from your ArbotiX-M. This sketch is also used by the DynaManager Software, useful for IDing your servos.



.. attention::
  If you are installing this firmware for use with the ROS kit, skip to the rest of the Firmware Section, Follow the instruction for IDing your Dynamixel Servos, and Follow the instruction in the Software for ROS section.
  
Firmware: ArmLink
^^^^^^^^^^^^^^^^^

  If you would like to control your WidowX arm over a USB connection to a computer using a simple graphic user interface, You might want to try loading the **InterbotixArmLinkSerial** Firmware and running the ArmLink Software.


Dynamixel Servo ID
------------------

.. raw:: html
  :url: http://www.trossenrobotics.com/Shared/readthedocs/dynamixelServoID.html


Software For ROS
----------------

  Install Xenial (Ubuntu 16.04.X LTS) on your machine. If you don't know how to do this, follow the directions on the `Ubuntu Website<https://www.ubuntu.com/download/desktop>`_ .

Software For ROS: Install Dev branch of GTK 3 for compilers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

  * sudo apt-get install build-essential libgtk-3-dev

Software For ROS: Install ROS Kinetic
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`Installation Instructions from ROS.org<http://wiki.ros.org/kinetic/Installation/Ubuntu>`_
  * sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

  * sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116

  * sudo apt update

  * sudo apt upgrade

  * sudo apt install ros-kinetic-desktop

  * sudo rosdep init

  * rosdep update

  * echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc

  * source ~/.bashrc

Software For ROS: RealSense ROS Package Install:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Prerequisites
  * wget -O enable_kernel_sources.sh http://bit.ly/en_krnl_src
  * bash ./enable_kernel_sources.sh

Sensor package
  * sudo apt install ros-kinetic-librealsense ros-kinetic-realsense-camera

  * sudo reboot

Kernel 4.10 installation work-around
  * sudo apt-get install libglfw3-dev

  * cd ~

  * git clone https://github.com/IntelRealSense/librealsense.git

  * cd librealsense

  * mkdir build && cd build

  * cmake ../

  * make && sudo make install

  * cd ..

  * sudo cp config/99-realsense-libusb.rules /etc/udev/rules.d/

  * sudo udevadm control --reload-rules && udevadm trigger

  * ./scripts/patch-realsense-ubuntu-xenial.sh

Software For ROS: Additional dependencies
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

  * sudo apt install git htop

  * sudo apt install ros-kinetic-moveit ros-kinetic-pcl-ros

Software For ROS: Setting dialout permission for Arbotix
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

  Replace *yourUserAccount* with the system account you are using
  * sudo usermod -a -G dialout yourUserAccount

  * sudo reboot

Software For ROS: Clone widowx_arm repository and build
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

  * mkdir -p ~/widowx_arm/src

  * cd ~/widowx_arm/src

  * git clone https://github.com/Interbotix/widowx_arm.git .

  * git clone https://github.com/Interbotix/arbotix_ros.git -b parallel_gripper

  * cd ~/widowx_arm

  * catkin_make

Software For ROS: Test execution without additional sensors
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

  * cd ~/widowx_arm

  * source devel/setup.bash

  * roslaunch widowx_arm_bringup arm_moveit.launch sim:=false sr300:=false

Software For ROS: Test execution with SR300 sensor
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

  * cd ~/widowx_arm

  * source devel/setup.bash

  * roslaunch widowx_arm_bringup arm_moveit.launch sim:=false sr300:=true
