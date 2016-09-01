FROM ubuntu:xenial
MAINTAINER Rex Tsai "https://about.me/chihchun"

ENV DEBIAN_FRONTEND=noninteractive
ENV BEIGNET_VERSION=1.1.1-2

RUN apt-get update \
 && apt-get dist-upgrade -y \
 && apt-get install -y beignet-opencl-icd=${BEIGNET_VERSION} clinfo

# Clean up APT when done
RUN apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
