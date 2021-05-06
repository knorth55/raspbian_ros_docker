FROM knorth55/raspbian_ros:assimp-3.3.1

ENV DEBIAN_FRONTEND=noninteractive

RUN echo "deb http://packages.ros.org/ros-testing/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list && \
    wget http://packages.ros.org/ros.key -O - | apt-key add - && \
    apt-get update && apt-get upgrade -y && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*

RUN apt-get update && apt-get install -y --no-install-recommends \
    python-rosdep \
    python-rosinstall-generator \
    python-wstool \
    python-rosinstall \
    python-catkin-tools && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*

RUN rosdep init && rosdep update

ARG ROS_DISTRO
RUN mkdir -p ~/ros/${ROS_DISTRO}/src && \
    cd ~/ros/${ROS_DISTRO}/src && \
    rosinstall_generator ros_comm --rosdistro ${ROS_DISTRO} --deps --wet-only --tar > .rosinstall && \
    wstool update -j 2 && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*

ARG ROS_DISTRO
RUN cd ~/ros/${ROS_DISTRO}/src && \
    rosdep update && apt-get update && \
    rosdep install -r -y -i --from-paths . --rosdistro ${ROS_DISTRO} --os=debian:stretch && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*
