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

- `knorth55/raspbian_ros:kinetic-latest` Raspbian stretch + Kinetic
- `knorth55/raspbian_ros:melodic-latest` Raspbian stretch + Melodic

## Usage

```bash
docker pull knorth55/raspbian_ros:kinetic-latest
docker run --rm -it --net=host --name <name> --env ROS_IP=<ip_address> --env ROS_MASTER_URI=http://<master_uri>:11311 knorth55/raspbian_ros:kinetic-latest /bin/bash
```

## Docker Installation on Raspberry Pi

```bash
curl -sSL https://get.docker.com | sh
sudo addgroup docker <username>
sudo systemctl start docker
```

### Installation error

**docker.service: Failed with result 'core-dump'**

Downgrade docker debian package.

`sudo apt-get install docker-ce=18.06.1~ce~3-0~raspbian`


## Docker image build on your computer 

### Dependency installation

`sudo apt install qemu-user-static`

### Build images

**ROS Kinetic**
```
git clone https://github.com/knorth55/raspbian_ros_docker.git
cd raspbian_ros_docker
docker build ./docker/assimp -t knorth55/raspbian_ros:assimp-3.3.1
docker build ./docker/rosdep -t knorth55/raspbian_ros:rosdep-kinetic-latest --build-arg ROS_DISTRO=kinetic
docker build ./docker/raspbian_ros -t knorth55/raspbian_ros:kinetic-latest --build-arg ROS_DISTRO=kinetic
```

**ROS Melodic**
```
git clone https://github.com/knorth55/raspbian_ros_docker.git
cd raspbian_ros_docker
docker build ./docker/assimp -t knorth55/raspbian_ros:assimp-3.3.1
docker build ./docker/rosdep -t knorth55/raspbian_ros:rosdep-melodic-latest --build-arg ROS_DISTRO=melodic
docker build ./docker/raspbian_ros -t knorth55/raspbian_ros:melodic-latest --build-arg ROS_DISTRO=melodic
```

## Test Environment

Raspberry Pi Zero HW + Docker
