1. create the following file: sudo nano /etc/udev/rules.d/99-uvc.rules with the content:
SUBSYSTEMS=="usb", ENV{DEVTYPE}=="usb_device", ATTRS{idVendor}=="32e4", ATTRS{idProduct}=="0234", MODE="0666"

2. reload the Udev rules:
sudo udevadm control --reload-rules

3. sudo apt-get install ros-noetic-libuvc-camera