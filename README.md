Steps to build QT static library for TV box running Armbian Linux. 

Armbian_bullseye.txt file includes some additional libaray files needed beyond https://doc.qt.io/qt-6/linux-building.html

Armbian Linux is from https://github.com/ophub/amlogic-s9xxx-armbian?tab=readme-ov-file

The QT static library is build with xcb build-in without need wayland

Build QT static library needs 4G memory. Although you can use "cmake --build . -j1" or "cmake --build . -j2" to limit parallel process, QT deson't follow the cmake rule at some stages. If you are using 1G or 2G memory TV box, it will run out of memory at some stage and cause the box not response. 

You can add additional swap file to increase the available memory. For examle, if you have 2G memory box, and 1G wap area, you will need at lease additional 2G swap file to increase the available memory to 5G. This will make the build success.

The step to add swap file is the following:

Check for existing swap space:  
   sudo swapon --show 
   free -h

Use fallocate to create a 2GB swap file: 
   sudo fallocate -l 2G /swapfile

Format the file as swap space:

   sudo mkswap /swapfile

Activate the swap file:

   sudo swapon /swapfile

If you want the swap file persistent after reboot:

  sudo nano /etc/fstab
  
  Add the following line to the end of the file:
  /swapfile swap swap defaults 0 0

Verify the swap is active:
  sudo swapon --show
  free -h
  

