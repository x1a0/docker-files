FROM ubuntu:16.04
MAINTAINER x1a0

RUN apt-get update && apt-get install -y \
  git \
  build-essential \
  libglib2.0-dev \
  libssl-dev

ARG BITLBEE_VERSION
ENV BITLBEE_VERSION ${BITLBEE_VERSION:-master}

WORKDIR /usr/src
RUN git clone https://github.com/bitlbee/bitlbee.git

WORKDIR /usr/src/bitlbee
RUN git checkout $BITLBEE_VERSION

RUN ./configure \
  --prefix=/usr \
  --etcdir=/etc/bitlbee \
  --ssl=openssl

RUN make && make install && make install-etc

RUN useradd \
  -m -d /var/lib/bitlbee \
  -s /usr/sbin/nologin \
  bitlbee

COPY bitlbee.conf /etc/bitlbee/bitlbee.conf

EXPOSE 6667
VOLUME /var/lib/bitlbee

WORKDIR /
ENTRYPOINT ["/usr/sbin/bitlbee", "-n"]
