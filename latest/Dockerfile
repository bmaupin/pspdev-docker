FROM ubuntu:18.04

ENV PSPDEV /usr/local/pspdev
ENV PATH ${PATH}:${PSPDEV}/bin

RUN \
  apt -y update && \
  # Workaround for https://askubuntu.com/q/909277/18665
  export DEBIAN_FRONTEND=noninteractive && \
  # From https://github.com/mrneo240/psptoolchain/blob/master/prepare.sh
  apt -y install autoconf automake bison build-essential bzip2 ca-certificates cmake doxygen flex gcc git gzip g++ libelf-dev libfreetype6-dev libncurses-dev libreadline-dev libusb-dev libtool subversion tcl texinfo wget xz-utils zlib1g-dev && \
  apt -y clean autoclean autoremove && \
  rm -rf /var/lib/{apt,dpkg,cache,log}/

RUN \
  git clone https://github.com/mrneo240/psptoolchain && \
  cd psptoolchain && \
  # Workaround for https://github.com/pspdev/psptoolchain/issues/74
  ln -sf bash /bin/sh && \
  ./toolchain-sudo.sh && \
  cd .. && \
  rm -Rf psptoolchain

WORKDIR /build
