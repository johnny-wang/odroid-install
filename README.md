## Overview

These are installation steps for Odroid XU4, Ubuntu 16.04, ROS Lunar, and OpenCV 3.3.

## Install Ubuntu 16.04

1. Download Ubuntu Mate image from
http://odroid.in/ubuntu_16.04lts/

2. un xz on your host with this command
```
ubuntu-16.04.3-4.9-mate-odroid-xu4-20170824.img.xz
```
3. Insert micro-SD Card to your host PC. Make sure your SD card is more than 8GB.

4. Install `Etcher` app on your PC to flash your SD card with a GUI.
https://etcher.io/

5. Remove the micro-SD card from your PC. 

6. Make sure Odroid is turned off and insert micro-SD card into Odroid.

7. Toggle the switch to boot from uSD card and power on Odroid.

8. Login to the Odroid (User:odroid, PW: odroid)

## Install tools

### apt lock error
If you get this error:
```
Could not get lock /var/lib/dpkg/lock - open (11 Resource temporarily unavailable)
```

It is because 16.04 automatically has a check for upgrades. To disable this, run:
```
$ sudo systemctl disable apt-daily.service # disable run when system boot
$ sudo systemctl disable apt-daily.timer   # disable timer run
```

### Install web browser

(Couldn't get Firefox to work properly)

```
sudo apt-get install chromium-browser
```

### Install VIM
```
sudo apt-get install vim
```

### Install git
```
sudo apt-get install git
```

## Install ROS Lunar
http://wiki.ros.org/Installation/UbuntuARM

1. Set up sources.list
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

2. Set up keys
```
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
```

3. Update
```
sudo apt-get update
```

4. Install everything
```
sudo apt-get install ros-lunar-desktop-full
```

## Install OpenCV

```
https://github.com/nanuyo/opencvsh_for_ubuntu_mate
```

1. Download or copy the opencv install script `opencv_install_to_ubuntu_mate_16.04.sh` from https://github.com/nanuyo/opencvsh_for_ubuntu_mate

2. Run the script
```
source opencv_install_to_ubuntu_mate_16.04.sh
```

3. Test facedetect sample
```
find . -name cpp-example-facedetect
```
```
cd build/bin/
./cpp-example-facedetect ../../samples/data/lena.jpg
```

## Setup Kinect 360

1. Install freenect
```
sudo apt-get install freenect python-freenect
```

2. Plug in your Kinect. You should see the device in `lsusb`

<img src="https://raw.githubusercontent.com/johnny-wang/odroid-install/master/images/kinect_lsusb.png" height="60%" width="60%">

2. Test freenect
```
free-nect-glview
```

A new window should pop up with a disparity and RGB view from the Kinect.

<img src="https://raw.githubusercontent.com/johnny-wang/odroid-install/master/images/kinect_test_view.png" height="60%" width="60%">

The command will also output some keystroke options you can use to control and test out various features of the Kinect.

<img src="https://raw.githubusercontent.com/johnny-wang/odroid-install/master/images/kinect_test_command.png" height="60%" width="60%">

## Troubleshooting

### Gstreamer build error
```
from /home/odroid/opencv_install/opencvsh_for_ubuntu_mate/OpenCV/opencv-3.3.0/modules/videoio/src/cap_gstreamer.cpp:67:
/usr/include/gstreamer-0.10/gst/pbutils/gstdiscoverer.h:35:9: error: ‘GstMiniObjectClass’ does not name a type
 typedef GstMiniObjectClass GstDiscovererStreamInfoClass;
```
https://stackoverflow.com/questions/30578381/failure-in-compiling-opencv-with-cap-gstreamer-error
```
sudo apt-get install
```
gstreamer prior to install is 0.10.36, after install is 1.11.91.

### Can't run facedetector

Look for facedetector example binary
Look for lena.jpg
```
find . -name facedetect
find . -name lena.jpg 
```
