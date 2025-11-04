FROM ubuntu:jammy

# custom golang image with CMake and Brotli support (compatible with ubuntu 18.04..22.04)

ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm-256color

RUN apt-get update && \
    apt-get -y install \
        build-essential cmake \
        iputils-ping \
        net-tools dnsutils \
        wget

RUN arch=$(arch | sed s/aarch64/arm64/ | sed s/x86_64/amd64/) && \
    wget -O - "https://go.dev/dl/go1.25.3.linux-${arch}.tar.gz" | tar -C /usr/local -xz && \
	export PATH="/usr/local/go/bin:$PATH" && \
	go version

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"

RUN arch=$(arch) && wget https://github.com/Kitware/CMake/releases/download/v4.1.2/cmake-4.1.2-linux-${arch}.tar.gz && \
    tar xf cmake-4.1.2-linux-${arch}.tar.gz -C /usr --strip-components=1

COPY submodules/ tmp/

RUN cd tmp/brotli && \
    mkdir out && cd out && \
    cmake .. && \
    make && make install
