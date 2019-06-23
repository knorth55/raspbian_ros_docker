FROM balenalib/rpi-raspbian:stretch
COPY qemu-arm-static /usr/bin

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y --no-install-recommends dirmngr gnupg2 lsb-release unzip wget

RUN echo "deb http://packages.ros.org/ros-testing/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list
RUN wget http://packages.ros.org/ros.key -O - | apt-key add -

RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
    build-essential \
    cmake \
    python-rosdep \
    python-rosinstall-generator \
    python-wstool \
    python-rosinstall \
    python-catkin-tools

RUN mkdir -p ~/libraries/assimp-3.3.1/build_release && \
    cd ~/libraries/assimp-3.3.1/ && \
    wget https://github.com/assimp/assimp/archive/v3.3.1.zip

RUN cd ~/libraries/assimp-3.3.1/ && \
    unzip v3.3.1.zip && mv assimp-3.3.1 src && \
    cd ~/libraries/assimp-3.3.1/build_release && \
    cmake ../src -DCMAKE_BUILD_TYPE=Release -DASSIMP_BUILD_TESTS=False && \
    make -j3 && make -j3 install && \
    rm ~/libraries/assimp-3.3.1/v3.3.1.zip

RUN rosdep init && rosdep update

ARG ROS_DISTRO
RUN mkdir -p ~/ros/${ROS_DISTRO}/src && \
    cd ~/ros/${ROS_DISTRO}/src && \
    rosinstall_generator ros_comm --rosdistro ${ROS_DISTRO} --deps --wet-only --tar > .rosinstall && \
    wstool update -j 2

RUN cd ~/ros/${ROS_DISTRO}/src && \
    rosdep install -u --from-paths . --ignore-src --rosdistro kinetic --os=debian:jessie -r -i -y

RUN cd ~/ros/${ROS_DISTRO}/src && \
    catkin build

RUN rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*
