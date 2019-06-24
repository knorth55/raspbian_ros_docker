# raspbian_ros_docker

[![GitHub version](https://badge.fury.io/gh/knorth55%2Fraspbian_ros_docker.svg)](https://badge.fury.io/gh/knorth55%2Fraspbian_ros_docker)
[![Build Status](https://travis-ci.com/knorth55/raspbian_ros_docker.svg?branch=master)](https://travis-ci.com/knorth55/raspbian_ros_docker)
[![Docker Stars](https://img.shields.io/docker/stars/knorth55/raspbian_ros.svg)](https://hub.docker.com/r/knorth55/raspbian_ros)
[![Docker Pulls](https://img.shields.io/docker/pulls/knorth55/raspbian_ros.svg)](https://hub.docker.com/r/knorth55/raspbian_ros)
[![Docker Automated](https://img.shields.io/docker/cloud/automated/knorth55/raspbian_ros.svg)](https://hub.docker.com/r/knorth55/raspbian_ros)
[![Docker Build Status](https://img.shields.io/docker/cloud/build/knorth55/raspbian_ros.svg)](https://hub.docker.com/r/knorth55/raspbian_ros)

## Usage

```
docker pull knorth55/raspbian_ros:kinetic-latest
docker run --rm -it --net=host --name <name> --env ROS_IP=<ip_address> --env ROS_MASTER_URI=http://<master_uri>:11311 knorth55/raspbian_ros:kinetic-latest /bin/bash
```
