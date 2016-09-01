FROM chihchun/opencl-intel
MAINTAINER Rex Tsai "https://about.me/chihchun"

ENV DEBIAN_FRONTEND=noninteractive
ENV OPENHASH_VERSION=v3.10

RUN echo "deb-src http://tw.archive.ubuntu.com/ubuntu/ yakkety restricted main universe multiverse" >> /etc/apt/sources.list.d/yakkety.list
RUN apt-get update \
 && apt-get install -y build-essential git \
 && apt-get build-dep -o APT::Get::Build-Dep-Automatic=true -y hashcat

WORKDIR /tmp
RUN git clone --depth 1 --branch $OPENHASH_VERSION \
        https://github.com/hashcat/hashcat.git \
 && cd hashcat \
 && make linux64 \
 && make install \
 && ln -s /usr/bin/hashcat64.bin /usr/bin/hashcat64

# Clean up APT when done
RUN apt-get purge -y build-essential git \
 && apt-get autoremove -y \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
