ARG ROS_DISTRO
FROM knorth55/raspbian_ros:rosdep-${ROS_DISTRO}-stretch-latest

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get upgrade -y && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*

ARG ROS_DISTRO
RUN cd ~/ros/${ROS_DISTRO} && catkin build -j 4
