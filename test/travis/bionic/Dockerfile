# This is the Dockerfile for testing problems in Travis build
# configuration #1.
# This needs not to be rebuild everytime, most of the time it needs just to
# be build once and then started when debugging issues and execute:
#   cd /AFLplusplus/
#   git pull
#   make distrib
#
FROM ubuntu:bionic
LABEL "about"="travis image 1"
RUN apt-get update && apt-get -y install \
    automake \
    bison \
    build-essential \
    clang \
    flex \
    git \
    python3.7 python3.7-dev \
    python3-setuptools \
    libtool libtool-bin \
    libglib2.0-dev \
    python-setuptools \
    wget \
    ca-certificates \
    libpixman-1-dev \
    gcc-7 gcc-7-plugin-dev libc++-7-dev \
    findutils \
    libcmocka-dev \
    joe nano vim locate \
    && rm -rf /var/lib/apt/lists/*

ENV AFL_NO_UI=1
ENV AFL_I_DONT_CARE_ABOUT_MISSING_CRASHES=1
ENV LLVM_CONFIG=llvm-config-6.0

RUN cd / && \
    git clone https://github.com/AFLplusplus/AFLplusplus && \
    cd AFLplusplus && \
    git checkout dev && \
    cd qemu_mode && wget http://download.qemu-project.org/qemu-3.1.1.tar.xz && \
    cd ../unicorn_mode && git submodule init && git submodule update || true && \
    cd /AFLplusplus && ASAN_BUILD=1 make source-only || true

WORKDIR /AFLplusplus
CMD ["/bin/bash"]
