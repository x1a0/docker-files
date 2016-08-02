FROM ubuntu:16.04
MAINTAINER x1a0

RUN apt-get update && apt-get install -y \
  git \
  build-essential \
  cmake \
  libgcrypt20-dev \
  libgnutls-dev \
  libcurl4-openssl-dev \
  libncurses-dev \
  libncursesw5-dev

ARG WEECHAT_VERSION
ENV WEECHAT_VERSION ${WEECHAT_VERSION:-master}

WORKDIR /usr/src
RUN git clone https://github.com/weechat/weechat.git

WORKDIR /usr/src/weechat
RUN git checkout $WEECHAT_VERSION

RUN mkdir build
WORKDIR /usr/src/weechat/build
RUN cmake .. \
  -DCMAKE_INSTALL_PREFIX=/usr

RUN make && make install

WORKDIR /
ENTRYPOINT ["/usr/bin/weechat"]
