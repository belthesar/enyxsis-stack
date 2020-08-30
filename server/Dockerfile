FROM debian:9.4

ENV DEBIAN_FRONTEND=noninteractive
ENV PACKETVER=20180418

WORKDIR /server

RUN apt-get update && apt-get -y install \
  make \
  g++ \
  mysql-client \
  mysql-server \
  default-libmysqlclient-dev \
  zlib1g-dev \
  libpcre3-dev \
  git

RUN git clone --shallow-since 2020-01-01 https://github.com/bryanveloso/rathena.git . \
  && git checkout renova

COPY ./wait.sh /server/wait.sh

RUN ./configure --enable-packetver=${PACKETVER} \
  && make clean \
  && make server \
  && groupadd -g 999 appuser \
  && useradd -r -u 999 -g appuser appuser \
  && chmod a+x /server/wait.sh \
  && chown appuser /server

USER appuser