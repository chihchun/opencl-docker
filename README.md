# Docker images that support different OpenCL Runtime

The images are designed to be easy tested applications with different OpenCL drivers/runtime.

- Support x86_64/amd64 platform.
- Ubuntu as based OS.

## Application

[hashcat](https://hashcat.net/hashcat/)

* [chihchun/hashcat-beignet](https://hub.docker.com/r/chihchun/hashcat-beignet/)
* [chihchun/hashcat-intel](https://hub.docker.com/r/chihchun/hashcat-intel/)

## Supported OpenCL platform

* Intel platform
    * [chihchun/opencl-beignet](https://hub.docker.com/r/chihchun/opencl-beignet/)

           Beignet is an open source implementation of the OpenCL specification - a generic compute oriented API. This code base contains the code to run OpenCL programs on Intel GPUs which basically defines and implements the OpenCL host functions required to initialize the device, create the command queues, the kernels and the programs and run them on the GPU.

           https://www.freedesktop.org/wiki/Software/Beignet/

    * [chihchun/opencl-intel](https://hub.docker.com/r/chihchun/opencl-intel/)

           Intel® SDK for OpenCL™ Applications 2016 R2 for Linux* (64 bit)
           OpenCL™ 2.0 Driver for Intel® HD, Iris™, and Iris™ Pro Graphics for Linux* (64-bit)
           https://software.intel.com/en-us/articles/opencl-drivers

* AMD/ATI Radeon (not tested)
    * [chihchun/opencl-mesa](https://hub.docker.com/r/chihchun/opencl-mesa/)

            Mesa (Gallium) https://dri.freedesktop.org/wiki/GalliumCompute/

* Nvidia (TBD)

## Usage

You need to expose the /dev/dri to the docker container, in order to let the runtime access to the GPU kernel interface.

    $ docker run -t -i --device /dev/dri:/dev/dri chihchun/opencl-beignet:1.1.1 clinfo
    $ docker run -t -i --device /dev/dri:/dev/dri \
            chihchun/hashcat-beignet hashcat -b

The Intel OpenCL Driver requires XCB-DRI2 authentication, which must be running in X11 enviroment. Please run the following docker command from Desktop. Intel OpenCL SDK requires 4.4.0 kernel with patches, the docker image has been tested with Ubuntu 16.04.

    % docker run -t -i --device /dev/dri:/dev/dri -v $(pwd)/wip:/mnt \
        -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY \
        chihchun/opencl-intel:2016R2 clinfo
