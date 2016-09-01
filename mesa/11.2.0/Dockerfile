FROM ubuntu:xenial
MAINTAINER Rex Tsai "https://about.me/chihchun"

ENV DEBIAN_FRONTEND=noninteractive
ENV MESA_VERSION=11.2.0-1ubuntu2.1

RUN apt-get update \
 && apt-get dist-upgrade -y \
 && apt-get install -y mesa-opencl-icd=${MESA_VERSION} clinfo

# Clean up APT when done
RUN apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
