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
  libncursesw5-dev \
  libperl-dev \
  libaspell-dev \
  python-dev \
  libv8-dev \
  tcl-dev \
  liblua5.2-dev \
  ruby-dev \
  guile-2.0-dev

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
ENV TERM xterm-256color
ENTRYPOINT ["/usr/bin/weechat"]
