FROM ubuntu:latest AS builder

WORKDIR /builder/working/directory
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates curl tar && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*

RUN curl -L https://github.com/balena-io/qemu/releases/download/v3.0.0%2Bresin/qemu-3.0.0+resin-arm.tar.gz | tar zxvf - -C . && mv qemu-3.0.0+resin-arm/qemu-arm-static .

FROM balenalib/rpi-raspbian:buster
COPY --from=builder /builder/working/directory/qemu-arm-static /usr/bin

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get upgrade -y && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    cmake \
    dirmngr \
    gnupg2 \
    lsb-release \
    tar \
    wget && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*

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
    rosdep update && \
    rosdep install --from-paths . --ignore-src --rosdistro ${ROS_DISTRO} --os=debian:buster -r -i -y && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*
