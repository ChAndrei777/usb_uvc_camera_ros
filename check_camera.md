
1. as a first step lets check what connected cams do we have:

![alt text](./pics/pic1.jpg)

2. Next install v4l-utils and get more info regarding supported formats: sudo apt install v4l-utils

3. v4l2-ctl --list-formats -d 0

![alt text](./pics/pic2.jpg)

video0 provides compressed images - highly likely framerate for this will be higher

4. now we check resolutions and frame rates
v4l2-ctl --list-formats-ext -d 0 
compressed images support different sizes and 90 fps max

![alt text](./pics/pic3.jpg)

uncompressed images framerate is not so high - and that is bad for robotics in case camera data is used inside demanding control loop

![alt text](./pics/pic4.jpg)

5. The following parameters are available in the camera for tuning:

![alt text](./pics/pic5.jpg)

6. With GStreamer we can try different resolutions and check latency. This command will open video and show it on the screen:
gst-launch-1.0 v4l2src device=/dev/video0 ! \
    image/jpeg,width=1280,height=720,framerate=90/1 ! \
    decodebin ! autovideosink

7. I am pretty much satisfied with image quality and latency at shown above config - now i would like to see how many LattePanda board resources (in terms of CPU and RAM) are consumed during GStreamer is active.
This is what htop shows when GStreamer is active

![alt text](./pics/pic6.jpg)

This is htop when GStreamer is inactive

![alt text](./pics/pic7.jpg)

Nearly 72% of one CPU core is consumed. Memory requirements are miniscular.