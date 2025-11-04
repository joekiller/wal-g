# vim:set ft=dockerfile:
FROM ubuntu:jammy

ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm-256color

# Configure apt and locale
RUN apt-get update -q && \
    apt-get install --yes --no-install-recommends --no-install-suggests \
    cmake build-essential wget ca-certificates && \
    rm -rf /var/lib/apt/lists/*

RUN arch=$(arch | sed s/aarch64/arm64/ | sed s/x86_64/amd64/) && \
    wget -O - "https://go.dev/dl/go1.25.2.linux-${arch}.tar.gz" | tar -C /usr/local -xz && \
	export PATH="/usr/local/go/bin:$PATH" && \
	go version

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"

RUN arch=$(arch) && wget https://github.com/Kitware/CMake/releases/download/v4.1.2/cmake-4.1.2-linux-${arch}.tar.gz && \
    tar xf cmake-4.1.2-linux-${arch}.tar.gz -C /usr --strip-components=1
