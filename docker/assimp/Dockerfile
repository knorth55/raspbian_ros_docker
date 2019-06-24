FROM ubuntu:latest AS builder

WORKDIR /builder/working/directory
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates curl tar
RUN curl -L https://github.com/balena-io/qemu/releases/download/v3.0.0%2Bresin/qemu-3.0.0+resin-arm.tar.gz | tar zxvf - -C . && mv qemu-3.0.0+resin-arm/qemu-arm-static .

FROM balenalib/rpi-raspbian:stretch
COPY --from=builder /builder/working/directory/qemu-arm-static /usr/bin

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y --no-install-recommends dirmngr gnupg2 lsb-release unzip wget

RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
    build-essential \
    cmake

RUN mkdir -p ~/libraries/assimp-3.3.1/build_release && \
    cd ~/libraries/assimp-3.3.1/ && \
    wget https://github.com/assimp/assimp/archive/v3.3.1.zip

RUN cd ~/libraries/assimp-3.3.1/ && \
    unzip v3.3.1.zip && mv assimp-3.3.1 src && \
    cd ~/libraries/assimp-3.3.1/build_release && \
    cmake ../src -DCMAKE_BUILD_TYPE=Release -DASSIMP_BUILD_TESTS=False && \
    make -j3 && make -j3 install && \
    rm ~/libraries/assimp-3.3.1/v3.3.1.zip

RUN rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*
