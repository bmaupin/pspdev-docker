# Build using ubuntu 16.04 since 18.04 throws a lot of errors building gcc 4.6.4
FROM ubuntu:16.04
MAINTAINER Naomi Peori <naomi@peori.ca>

ENV PSPDEV /usr/local/pspdev
ENV PATH ${PATH}:${PSPDEV}/bin

RUN \
  apt -y update && \
  apt -y install autoconf bison build-essential cmake doxygen flex git libarchive-dev libcurl4-openssl-dev libgpgme11-dev libncurses5-dev libreadline-dev libsdl1.2-dev libssl-dev libtool-bin libusb-dev python3 subversion tcl texinfo unzip wget zlib1g-dev && \
  apt -y clean autoclean autoremove && \
  rm -rf /var/lib/{apt,dpkg,cache,log}/

RUN \
  git clone https://github.com/pspdev/psptoolchain && \
  cd psptoolchain && \
  # Workaround for https://github.com/pspdev/psptoolchain/issues/98
  sed 's/4.9.3/4.6.4/' -i scripts/00?-gcc-stage?.sh && \
  # Workaround for "The authenticity of host 'github.com (140.82.113.4)' can't be established."
  mkdir -p ~/.ssh && \
  ssh-keyscan -H github.com >> ~/.ssh/known_hosts && \
  # Workaround for https://github.com/pspdev/psptoolchain/issues/74
  ln -sf bash /bin/sh && \
  ./toolchain.sh && \
  cd .. && \
  rm -Rf psptoolchain

WORKDIR /build
