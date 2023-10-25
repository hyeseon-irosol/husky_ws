# HUSKY_WS 

This workspace has Dockerfile for operating both the Husky robot and simulation in Gazebo.

## Installation

```bash
$ git clone https://github.com/hyeseon-irosol/husky_ws.git
```

## How to use the packages from [Tinker-Twins](https://github.com/Tinker-Twins/Husky).

1. Keyboard Teleoperation:
    ```bash
    $ roslaunch husky_gazebo husky_playpen.launch
    $ roslaunch husky_control teleop_keyboard.launch
    ```

2. Map-Less Navigation:
    ```bash
    $ roslaunch husky_gazebo husky_playpen.launch
    $ roslaunch husky_viz view_robot.launch
    $ roslaunch husky_navigation map_less_navigation.launch
    ```

3. Simultaneous Localization And Mapping (SLAM):
    ```bash
    $ roslaunch husky_gazebo husky_playpen.launch
    $ roslaunch husky_viz view_robot.launch
    $ roslaunch husky_navigation gmapping.launch
    $ roslaunch husky_control teleop_keyboard.launch
    ```
    To save generated map to current working directory, run:
    ```bash
    $ rosrun map_server map_saver -f <filename>
    ```

4. Adaptive Monte Carlo Localization (AMCL):
    ```bash
    $ roslaunch husky_gazebo husky_playpen.launch
    $ roslaunch husky_viz view_robot.launch
    $ roslaunch husky_navigation amcl.launch
    $ roslaunch husky_control teleop_keyboard.launch
    ```

5. Map-Based Navigation:
    ```bash
    $ roslaunch husky_gazebo husky_playpen.launch
    $ roslaunch husky_viz view_robot.launch
    $ roslaunch husky_navigation map_based_navigation.launch
    ```

## Network setting

Please connect with the same wifi network Husky using which is "ASUS_ROUTER".

If you want to run the simulation Husky in Gazebo, the ROS_MASTER_URI should be another IP address, not Husky IP address.
In the Dockerfile, the address might be chagned from your own IP address. Please check it using "ifconfig"
:
RUN echo "export ROS_MASTER_URI=http://YOUR_IP_ADDRESS:11311" >> /home/${USERNAME}/.bashrc
