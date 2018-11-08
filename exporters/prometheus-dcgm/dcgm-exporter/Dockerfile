FROM ubuntu:16.04

RUN apt-get update && apt-get install -y make build-essential autoconf libtool pkg-config  libgflags-dev libgtest-dev clang libc++-dev git && \ 
rm -rf /var/lib/apt/lists/*

RUN cd /tmp && \
git clone --recursive https://github.com/grpc/grpc && \
cd grpc && \
git fetch origin && \
# pick up changes in https://github.com/grpc/grpc/pull/16766
# change this once it is released in v1.17.0
git checkout 191766c0f21dc43d0928bb5ab70f73df54ba5701 && \
make && \
make install && \
make grpc_cli && \
cp /tmp/grpc/bins/opt/grpc_cli /usr/local/bin/ && \
rm -rf /tmp/grpc

COPY api.proto /tmp/api.proto

ARG DCGM_VERSION=1.4.6

COPY datacenter-gpu-manager_${DCGM_VERSION}_amd64.deb /tmp
RUN dpkg -i /tmp/*.deb && rm -f /tmp/*

COPY dcgm-exporter /usr/local/bin

ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES utility

VOLUME /run/prometheus

ENTRYPOINT [ "dcgm-exporter", "-e" ]
