FROM osrf/ros:noetic-desktop-full

ARG USERNAME=husky_docker
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
  && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
  && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
  && chmod 0440 /etc/sudoers.d/$USERNAME  

USER $USERNAME
ENV USER=$USERNAME
WORKDIR /home/$USERNAME

# Update and install necessary packages
RUN sudo apt-get update && \
    sudo apt-get install -y git \
    nano \
    python3-roslaunch \
    iputils-ping \
    net-tools \
    ros-noetic-navigation \
    ros-noetic-slam-gmapping \
    ros-noetic-husky-desktop \
    ros-noetic-husky-simulator \
    ros-noetic-fath-pivot-mount-description \
    ros-noetic-flir-camera-description \
    ros-noetic-velodyne-description \
    ros-noetic-realsense2-description \
    ros-noetic-lms1xx \
    ros-noetic-robot-localization \
    ros-noetic-interactive-marker-twist-server \
    ros-noetic-twist-mux \
    ros-noetic-teleop-twist-keyboard \
    ros-noetic-teleop-twist-joy \
    ros-noetic-rviz-imu-plugin \
    ros-noetic-gmapping

# Create a workspace
RUN mkdir workspace
WORKDIR /home/$USERNAME/workspace
RUN mkdir src
WORKDIR /home/$USERNAME/workspace/src

# Clone Husky packages into the workspace
RUN git clone https://github.com/Tinker-Twins/Husky.git

# Network setting for connecting Husky Robot
RUN echo "export ROS_MASTER_URI=http://192.168.50.122:11311" >> /home/${USERNAME}/.bashrc
# Network setting for husky simulation in Gazebo. The IP address might be different with your own.
#RUN echo "export ROS_MASTER_URI=http://192.168.50.60:11311" >> /home/${USERNAME}/.bashrc

# Build the workspace
RUN [ "/bin/bash" , "-c" , "cd /home/$USERNAME/workspace && source /opt/ros/noetic/setup.sh && catkin_make -j4"]

RUN echo "source /opt/ros/noetic/setup.sh" >> /home/$USERNAME/.bashrc
RUN echo "source /home/$USERNAME/workspace/devel/setup.sh" >> /home/$USERNAME/.bashrc