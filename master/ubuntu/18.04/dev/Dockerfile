FROM ubuntu:18.04

RUN apt-get update && \
    apt-get install -y software-properties-common
RUN add-apt-repository ppa:ubuntu-toolchain-r/test

RUN apt-get update && \
    apt-get install -y \
            autoconf \
            automake \
            autotools-dev \
            build-essential \
            curl \
            dpkg-dev \
            git \
            gnupg \
            imagemagick \
            iputils-ping \
            ispell \
            libacl1-dev \
            libasound2-dev \
            libcanberra-gtk3-module \
            libdbus-1-dev \
            libgif-dev \
            libgnutls28-dev \
            libgpm-dev \
            libgtk-3-dev \
            libjansson-dev \
            libjpeg-dev \
            liblcms2-dev \
            liblockfile-dev \
            libm17n-dev \
            libmagick++-6.q16-dev \
            libncurses5-dev \
            libotf-dev \
            libpng-dev \
            librsvg2-dev \
            libselinux1-dev \
            libtiff-dev \
            libxaw7-dev \
            libxml2-dev \
            openssh-client \
            texinfo \
            wget \
            xaw3dg-dev \
    zlib1g-dev \
    gcc-10 g++-10 libgccjit0 libgccjit-10-dev libjansson4 libjansson-dev \
    && rm -rf /var/lib/apt/lists/*

ADD https://git.sv.gnu.org/git/emacs.git/refs/heads/master /tmp/cache

RUN git clone --depth 1 --branch master git://git.sv.gnu.org/emacs.git /opt/emacs && \
    cd /opt/emacs && \
    ./autogen.sh && \
    CC=/usr/bin/gcc-10 CXX=/usr/bin/gcc-10 ./configure --build="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" --with-modules --with-native-compilation && \
    make && \
    make install

RUN mkdir -p /root/.emacs.d/elpa/gnupg && \
    chmod 700 /root/.emacs.d/elpa/gnupg && \
    for i in {1..3}; do \
      gpg --keyserver keyserver.ubuntu.com \
          --homedir /root/.emacs.d/elpa/gnupg \
          --recv-keys 066DAFCB81E42C40 \
      && break || sleep 15; \
    done

CMD ["emacs"]
