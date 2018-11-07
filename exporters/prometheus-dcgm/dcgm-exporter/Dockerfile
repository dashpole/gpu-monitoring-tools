FROM ubuntu:16.04

RUN apt-get update && apt-get install -y curl make build-essential autoconf libtool pkg-config libgflags-dev libgtest-dev clang libc++-dev make libgoogle-perftools-dev zlib1g-dev libc-ares-dev unzip libssl-dev g++ && rm -rf /var/lib/apt/lists/*

RUN curl -OL https://github.com/google/protobuf/releases/download/v3.6.1/protoc-3.6.1-linux-x86_64.zip && unzip protoc-3.6.1-linux-x86_64.zip -d protoc3 && mv protoc3/bin/* /usr/local/bin/ && mv protoc3/include/* /usr/local/include/ && rm -rf protoc3

RUN mkdir grpc && curl -sSL https://github.com/grpc/grpc/tarball/v1.16.0 | tar -v -C . -xz && cd grpc-grpc-98457b7

RUN cd grpc-grpc-98457b7 && make run_dep_checks
RUN cd grpc-grpc-98457b7 && make
#COPY grpc-grpc-98457b7/bins/opt/grpc_cli /usr/local/bin

#ARG DCGM_VERSION=1.4.6

#COPY datacenter-gpu-manager_${DCGM_VERSION}_amd64.deb /tmp
#RUN dpkg -i /tmp/*.deb && rm -f /tmp/*

#COPY dcgm-exporter /usr/local/bin

#ENV NVIDIA_VISIBLE_DEVICES all
#ENV NVIDIA_DRIVER_CAPABILITIES utility

#VOLUME /run/prometheus

#ENTRYPOINT [ "dcgm-exporter", "-e" ]
