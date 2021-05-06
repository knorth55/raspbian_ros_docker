# raspbian_ros_docker

[![GitHub version](https://badge.fury.io/gh/knorth55%2Fraspbian_ros_docker.svg)](https://badge.fury.io/gh/knorth55%2Fraspbian_ros_docker)
[![Docker Stars](https://img.shields.io/docker/stars/knorth55/raspbian_ros.svg)](https://hub.docker.com/r/knorth55/raspbian_ros)
[![Docker Pulls](https://img.shields.io/docker/pulls/knorth55/raspbian_ros.svg)](https://hub.docker.com/r/knorth55/raspbian_ros)
[![Docker Automated](https://img.shields.io/docker/cloud/automated/knorth55/raspbian_ros.svg)](https://hub.docker.com/r/knorth55/raspbian_ros)
[![Docker Build Status](https://img.shields.io/docker/cloud/build/knorth55/raspbian_ros.svg)](https://hub.docker.com/r/knorth55/raspbian_ros)

## Description

Raspbian + ROS docker image for Raspberry Pi

**If you have Raspberry Pi 2 or 3, I recommend to install Ubuntu Mate + ROS.**

## Docker images

Docker images are distributed in [Dockerhub knorth55/raspbian_ros](https://hub.docker.com/r/knorth55/raspbian_ros)

- `knorth55/raspbian_ros:melodic-buster-latest` Raspbian buster + Melodic
- `knorth55/raspbian_ros:melodic-stretch-latest` Raspbian stretch + Melodic
- `knorth55/raspbian_ros:kinetic-stretch-latest` Raspbian stretch + Kinetic

## Usage

```bash
docker pull knorth55/raspbian_ros:melodic-buster-latest
docker run --rm -it --net=host --name <name> --env ROS_IP=<ip_address> --env ROS_MASTER_URI=http://<master_uri>:11311 knorth55/raspbian_ros:melodic-buster-latest /bin/bash
```

## Docker Installation on Raspberry Pi

### Installation

```bash
curl -sSL https://get.docker.com | sh
sudo addgroup docker <username>
sudo systemctl start docker
```

## Docker image build on your computer 

### Dependency installation

`sudo apt install qemu-user-static`

### Build images

#### Raspbian buster + ROS Melodic
```
git clone https://github.com/knorth55/raspbian_ros_docker.git
cd raspbian_ros_docker
docker build ./docker/buster/rosdep -t knorth55/raspbian_ros:rosdep-melodic-buster-latest --build-arg ROS_DISTRO=melodic
docker build ./docker/buster/raspbian_ros -t knorth55/raspbian_ros:melodic-buster-latest --build-arg ROS_DISTRO=melodic
```

#### Raspbian stretch + ROS Melodic
```
git clone https://github.com/knorth55/raspbian_ros_docker.git
cd raspbian_ros_docker
docker build ./docker/stretch/assimp -t knorth55/raspbian_ros:assimp-3.3.1
docker build ./docker/stretch/rosdep -t knorth55/raspbian_ros:rosdep-melodic-stretch-latest --build-arg ROS_DISTRO=melodic
docker build ./docker/stretch/raspbian_ros -t knorth55/raspbian_ros:melodic-stretch-latest --build-arg ROS_DISTRO=melodic
```

#### Raspbian stretch + ROS Kinetic
```
git clone https://github.com/knorth55/raspbian_ros_docker.git
cd raspbian_ros_docker
docker build ./docker/stretch/assimp -t knorth55/raspbian_ros:assimp-3.3.1
docker build ./docker/stretch/rosdep -t knorth55/raspbian_ros:rosdep-kinetic-stretch-latest --build-arg ROS_DISTRO=kinetic
docker build ./docker/stretch/raspbian_ros -t knorth55/raspbian_ros:kinetic-stretch-latest --build-arg ROS_DISTRO=kinetic
```

## Test Environment

Raspberry Pi Zero HW + Docker

## FAQ

### Installation error

**docker.service: Failed with result 'core-dump'**

Downgrade docker debian package.

`sudo apt-get install docker-ce=18.06.1~ce~3-0~raspbian`
