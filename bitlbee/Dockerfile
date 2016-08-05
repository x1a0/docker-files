FROM ubuntu:16.04
MAINTAINER x1a0

RUN apt-get update && apt-get install -y \
  git \
  build-essential \
  autoconf \
  libglib2.0-dev \
  libssl-dev \
  libevent-dev \
  libtool \
  libjson-glib-dev

#
# Install BitlBee
#

ARG BITLBEE_VERSION
ENV BITLBEE_VERSION ${BITLBEE_VERSION:-master}

WORKDIR /usr/src
RUN git clone https://github.com/bitlbee/bitlbee.git

WORKDIR /usr/src/bitlbee
RUN git checkout $BITLBEE_VERSION

RUN ./configure \
  --prefix=/usr \
  --etcdir=/etc/bitlbee \
  --ssl=openssl \
  --events=libevent

RUN make \
  && make install \
  && make install-etc \
  && make install-dev

RUN useradd \
  -m -d /var/lib/bitlbee \
  -s /usr/sbin/nologin \
  bitlbee

COPY bitlbee.conf /etc/bitlbee/bitlbee.conf


#
# Install BitlBee Facebook Plugin
#

ARG BITLBEE_FB_VERSION
ENV BITLBEE_FB_VERSION ${BITLBEE_FB_VERSION:-master}

WORKDIR /usr/src
RUN git clone https://github.com/bitlbee/bitlbee-facebook.git

WORKDIR /usr/src/bitlbee-facebook
RUN git checkout $BITLBEE_FB_VERSION

RUN ./autogen.sh \
  && make \
  && make install


EXPOSE 6667
VOLUME /var/lib/bitlbee
RUN chown -R bitlbee:bitlbee /var/lib/bitlbee

WORKDIR /
ENTRYPOINT ["/usr/sbin/bitlbee", "-n"]
