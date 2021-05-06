ARG ROS_DISTRO
FROM knorth55/raspbian_ros:rosdep-${ROS_DISTRO}-buster-latest

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get upgrade -y && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*

ARG ROS_DISTRO
# https://gitlab.kitware.com/cmake/cmake/-/issues/20568
RUN cd ~/ros/${ROS_DISTRO} && catkin build -j 4 -DCMAKE_BUILD_TYPE=Release -D_FILE_OFFSET_BITS=64
