FROM chihchun/opencl-beignet:latest
MAINTAINER Rex Tsai "https://about.me/chihchun"

ENV DEBIAN_FRONTEND=noninteractive
ENV HASHCAT_VERSION=3.00-3

RUN apt-get update \
 && apt-get -y install hashcat=${HASHCAT_VERSION}

# Clean up APT when done
RUN apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
