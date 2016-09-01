FROM ubuntu:yakkety
MAINTAINER Rex Tsai "https://about.me/chihchun"

ENV DEBIAN_FRONTEND=noninteractive
ENV MESA_VERSION=12.0.1-3ubuntu2

RUN apt-get update \
 && apt-get dist-upgrade -y \
 && apt-get install -y mesa-opencl-icd=${MESA_VERSION} clinfo

# Clean up APT when done
RUN apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
