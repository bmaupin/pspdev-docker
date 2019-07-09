FROM ubuntu:16.04
MAINTAINER Naomi Peori <naomi@peori.ca>

ENV PSPDEV /usr/local/pspdev
ENV PATH ${PATH}:${PSPDEV}/bin

RUN \
  apt-get -y update && \
  apt-get -y install autoconf bison build-essential cmake doxygen flex git libncurses5-dev libreadline-dev libsdl1.2-dev libtool-bin libusb-dev subversion tcl texinfo unzip wget zlib1g-dev && \
  apt-get -y clean autoclean autoremove && \
  rm -rf /var/lib/{apt,dpkg,cache,log}/

RUN \
  git clone https://github.com/pspdev/psptoolchain && \
  cd psptoolchain && \
  # Workaround for https://github.com/pspdev/psptoolchain/issues/98
  sed 's/4.9.3/4.6.4/' -i scripts/00?-gcc-stage?.sh && \
  # Fix for "The authenticity of host 'github.com (140.82.113.4)' can't be established."
  mkdir -p ~/.ssh && \
  ssh-keyscan -H github.com >> ~/.ssh/known_hosts && \
  ./toolchain.sh && \
  cd .. && \
  rm -Rf psptoolchain

WORKDIR /build
