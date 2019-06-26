FROM knorth55/raspbian_ros:assimp-3.3.1

ENV DEBIAN_FRONTEND=noninteractive

RUN echo "deb http://packages.ros.org/ros-testing/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list
RUN wget http://packages.ros.org/ros.key -O - | apt-key add -

RUN apt-get update && apt-get upgrade -y
RUN apt-get update && apt-get install -y --no-install-recommends \
    python-rosdep \
    python-rosinstall-generator \
    python-wstool \
    python-rosinstall \
    python-catkin-tools

RUN rosdep init && rosdep update

ARG ROS_DISTRO
RUN mkdir -p ~/ros/${ROS_DISTRO}/src && \
    cd ~/ros/${ROS_DISTRO}/src && \
    rosinstall_generator ros_comm --rosdistro ${ROS_DISTRO} --deps --wet-only --tar > .rosinstall && \
    wstool update -j 2

RUN cd ~/ros/${ROS_DISTRO}/src && \
    rosdep install --from-paths . --ignore-src --rosdistro kinetic --os=debian:jessie -r -i -y

RUN cd ~/ros/${ROS_DISTRO} && catkin build -j 4

RUN rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*
