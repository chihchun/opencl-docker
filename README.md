# Docker images that support differnt OpenCl Runtime

The images are designed to be easy tested applications with differnet OpenCL drivers/runtime.

- Support x86_64/amd64 platform.
- Ubuntu as based OS.

## Application

* chihchun/hashcat-beignet https://hashcat.net/hashcat/

## Supported OpenCL platform

* Intel platform
    * chihchun/opencl-beignet https://www.freedesktop.org/wiki/Software/Beignet/
* AMD/ATI Radeon (not tested)
    * chihchun/opencl-mesa http://mesa3d.sourceforge.net/
* Nvidia (TBD)

## Usage

You need to expose the /dev/dri to the docker container, in order to let the runtime access to the GPU kernel interface.

    $ docker run -t -i --device /dev/dri:/dev/dri chihchun/opencl-beignet:1.1.1 clinfo
    $ docker run -t -i --device /dev/dri:/dev/dri \
            chihchun/hashcat-beignet hashcat -b
