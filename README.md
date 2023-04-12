# ros2-examples-ads
Example ROS2 package for communicating with Beckhoff PLC´s using ADS/AMS.

ADS - Automation Device Specification<br />
AMS - Automation Message Specification

See also:
https://infosys.beckhoff.com/content/1033/tc3_ads_intro/116158859.html


<br />
Tested using Ubuntu 22.04.2 LTS.

<br /><br />
Build instructions for ADS library (do this first):

1. Navigate to a suitable location, for example `cd ~/projects/`.
2. Clone the project _including submodules_ in your selected location:
<br />`git clone --recurse-submodules git@github.com:kristianmk/ros2-examples-ads.git`. (or https://github.com/kristianmk/ros2-examples-ads.git)
3. Go to the ADS subfolder; build the ADS library. Build as described in the ADS library README-file: First `meson build` then `ninja -C build`. Error-like message "Library&nbsp;ws2_32&nbsp;found:&nbsp;NO" is OK when we are running meson build on Linux, as ws2_32 is the MS Windows sockets library (we don´t need/want that anyways).
4. Go back to the main ros-examples-ads folder.

The Beckhoff ADS library is available here if you prefer not to use submodules: https://github.com/Beckhoff/ADS .


<br /><br />
Build instructions for ADS example without ROS2 (example more or less identical to the official Beckhoff example program):

1. Navigate to the `ads_example_cmake_no_ros2` folder.
2. Edit the ADS example to reflect a correct remote IP and remote AMS net id.
3. Run `cmake .` then `make`.
4. Test the ads_example program.


<br /><br />
Build instructions for ROS2 node example:

0. Make sure you have ROS2 installed.
1. Navigate to the `ads_example_package` folder.
2. Edit the ADS example to reflect a correct remote IP and remote AMS net id.
3. Source ROS2 underlay (for example if using a bash terminal and a custom built ROS2: <br />`. ~/ros2_humble/install/local_setup.bash`.
4. Build using `colcon build`.
5. Source ROS2 overlay (for example, if using a bash terminal: `. install/local_setup.bash`.
6. Run the node with `ros2 run ads_example_package ads_node`.

Exception handling was not included in this example; all ADS operations that could throw exceptions should be handled; see error handling in the ADS example without ROS2 from Beckhoff. See https://isocpp.org/wiki/faq/exceptions#why-exceptions to understand why you should know exceptions in C++.
