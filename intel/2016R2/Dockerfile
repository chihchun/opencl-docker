FROM ubuntu:xenial
MAINTAINER Rex Tsai "https://about.me/chihchun"

ENV DEBIAN_FRONTEND=noninteractive

# OpenCL™ 2.0 Driver for Intel® HD, Iris™, and Iris™ Pro Graphics for Linux* (64-bit)
ENV INTEL_DRIVER_URL=http://registrationcenter-download.intel.com/akdlm/irc_nas/9418/intel-opencl-2.0-2.0-54425.tar.gz
# Intel® SDK for OpenCL™ Applications 2016 R2 for Linux* (64 bit)
ENV INTEL_SDK_URL=http://registrationcenter-download.intel.com/akdlm/irc_nas/9553/intel_sdk_for_opencl_2016_ubuntu_6.2.0.1760_x64.tgz

RUN apt-get update \
 && apt-get dist-upgrade -y \
 && apt-get install -y --no-install-recommends alien wget tar \
 && apt-get install -y clinfo \
 && apt-get install -y libxcb-dri3-0 libxcb-dri2-0

WORKDIR /tmp
RUN wget ${INTEL_DRIVER_URL} \
 && wget ${INTEL_SDK_URL}

# Install Driver
RUN TARBALL=$(basename ${INTEL_DRIVER_URL}) \
 && DIR=$(basename ${INTEL_DRIVER_URL} .tar.gz) \
 && tar zxvf ${TARBALL} \
 && for i in ${DIR}/*rpm ; do alien --to-deb $i ; done

# Install SDK
RUN TARBALL=$(basename ${INTEL_SDK_URL}) \
 && DIR=$(basename ${INTEL_SDK_URL} .tgz) \
 && tar zxvf ${TARBALL} \
 && for i in ${DIR}/rpm/*.rpm ; do alien --to-deb $i ; done

# Install the debian packages.
RUN dpkg -i *.deb

# Clean up APT when done
RUN apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
