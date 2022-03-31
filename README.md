# ros2-examples-ads
Example ROS2 package for communicating with Beckhoff PLC´s using ADS/AMS.

ADS - Automation Device Specification
AMS - Automation Message Specification

See also:
https://infosys.beckhoff.com/english.php?content=../content/1033/tcadsamsspec/html/tcadsamsspec_intro.htm



Tested using Ubuntu 20.04.4 LTS.


Build instructions for ADS library (do this first):

1. Navigate to a suitable location, for example `cd ~/projects/`.
2. Clone the project _including submodules_ in your selected location:
`git clone --recurse-submodules git@github.com:kristianmk/ros2-examples-ads.git`.
3. Go to the ADS subfolder; build the ADS library. First `meson build` then `ninja -C build`. Error-like message "Library&nbsp;ws2_32&nbsp;found:&nbsp;NO" is OK when we are running meson build on Linux, as ws2_32 is the MS Windows sockets library (we don´t need/want that anyways).
4. Go back to the main ros-examples-ads folder.


Build instructions for ADS example without ROS2:

1. Navigate to the `ads_example_cmake_no_ros2` folder.
2. Edit the ADS example to reflect a correct remote IP and remote AMS net id.
3. Run `cmake .` then `make`.
`git clone --recurse-submodules git@github.com:kristianmk/ros2-examples-ads.git`.
4. Test the ads_example program.
