This is the config (/boot/config.txt) file used for using sensors with GrovePi+. 

There were several issues before GrovePi+ worked with Raspberry 4. They were resolved and here are the solutions.

1. First check if some option is not blocking GPIOs etc. 

Some sensors were not working becasue video drivers etc block some interfaces and gpio pins. Thus:

  - disable SPI 

`dtparam=spi=off`

- comment the following lines if they exist to disable video driver (it was present 2 times in the file) and gpio8 use (it is needed to be free for GrovePi+):

`#dtoverlay=vc4-fkms-v3d`

`#dtoverlay=vc4-fkms-v3d`

`#gpio=8=op,dh`

2. Most problems happened after dist-upgrade or upgrading the system with sudo apt-get upgrade.

GrovePi+ firmware update started giving the following error after sudo bash firmware_update.sh:

gpio/direction: No such file or directory

ardude done. Thank you.

Thus, perhaps one way is to not upgrade the system. Otherwise the following solutions work.

3. Solutions

- Comment the options and disable SPI as explained in step 1. Reboot (sometimes need to disconnect the power).

- See if any gpio is not blocked
sudo cat /sys/kernel/debug/gpio

- Versions of avrdude and gpio tools which were tested and work are:
avrdude version 5.10, gpio version 2.60


