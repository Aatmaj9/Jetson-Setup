# Setting up Jetson Nano

Requirements :
Monitor , Micro usb to usb for powering on jetson , hdmi cable for viewing jetson on monitor , SD card , Ethernet cable ( Router if required)

## Part 1 - Install Jetson OS 

### Method 1 - SD Card Image Method

#### Step1 : Flash the image on SD card 

Insert SD card in your laptop and download the image for nvidia website. Flash the image on the SD card using a flashing tool ( rufus )

More clarification regarding the image - 

JetPack includes Jetson Linux with bootloader, Linux kernel, Ubuntu desktop environment, and a complete set of libraries for acceleration of GPU computing, multimedia, graphics, and computer vision. It also includes samples, documentation, and developer tools for both host computer and developer kit, and supports higher level SDKs such as DeepStream for streaming video analytics, Isaac for robotics, and Riva for conversational AI. 

For Jetson Orin nano we downloaded Jetpack 5.1.1( as we were using ros1 )
It includes Jetson Linux 35.4.1 BSP with Linux Kernel 5.10, an Ubuntu 20.04 based root file system, a UEFI based bootloader, and OP-TEE as Trusted Execution Environment.
You can download it from here- 

https://developer.nvidia.com/embedded/jetpack-sdk-511

Note : If you want to upgrade to ROS 2 later we have to install Jetpack 6 which includes Jetson linux 36.2 which packs kernel 5.15 and Ubuntu 22.04 based root system.

https://developer.nvidia.com/embedded/jetpack-sdk-60dp 

Here we will be working on Jetpack 5.1.1 with Ubuntu 20.04 and ROS Npo

#### Step2 :  

Insert the SD card in jetson. Connect jetson to power source and ethernet for internet . Connect monitor and jetson using HDMI cable. Go through the initial setup on screen.
You can see Jetson OS on the monitor.

### Method 2 - SDK Manager

Note: You can also use the SDK manager on a host linux system to flash the image in jetson. It is easier to do as it shows the Jetson device as well as the recommended Jetpack for the device. Connect jetson to the host computer using the usb or usb c port on the Jetson.

## Part 2 - Setting up SSH

#### Step 1 : Downloading SSH

You have to download SSH on your laptop and jetson. Connect the jetson  to power source, monitor and ethernet.

Open terminal on jetson and install SSH using command

```
sudo apt-get install openssh-server
```

Now we have SSH installed on our jetson. To use it remotely we need to connect jetson with our laptop for that we need a static ip address of our jetson.

#### Step 2 : Connecting to Jetson

From routers website obtain jetsons ip address

192.168.0.1  - this is the router website for d-link you can see the Jetsons ip there

Connect laptop to jetson using SSH.

Open the linux terminal on your laptop. Make sure the Jetson and laptop are connected to the same network .

```
ssh -X <Username>@<Your_Jetson_IP>
```

Replace username with jetsons username and ip address you got.
You will be prompted to input the Jetson Nanos Password.
You now have remote access to your jetson nano.

Important points to note:
Use proper USB b cable for jetson nano. 
If lan port is not available near monitor use wifi router and long ethernet cables to connect them ( This is for jetsons without wifi module )

# Installing ROS Noetic on Jetson Nano

Follow the same steps as installing ROS Noetic on ubuntu 20.04

Follow this -
http://wiki.ros.org/noetic/Installation/Ubuntu

Now make a catkin workspace and catkin package named arduino_comm with rospy roscpp and std_msgs as dependencies. If you dont remember let us see how to do this -

```
source /opt/ros/noetic/setup.bash
mkdir -p ~/amogh_ws/src
cd ~/amogh_ws
catkin_make
source devel/setup.bash
cd ~/amogh_ws/src
catkin_create_pkg arduino_comm std_msgs rospy roscpp
cd ~/amogh_ws
catkin_make
source devel/setup.bash
```
