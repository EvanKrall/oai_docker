FROM ubuntu:14.04
RUN apt-get update && apt-get install -yq \
    autoconf \ 
    automake \ 
    bison \ 
    build-essential \ 
    check \ 
    cmake \ 
    cmake-curses-gui \ 
    doxygen \ 
    doxygen-gui \ 
    ethtool \ 
    flex \ 
    gcc \ 
    gccxml \ 
    gdb \ 
    git \ 
    guile-2.0-dev \ 
    iperf \ 
    iproute \ 
    libconfig8-dev \ 
    libgcrypt11-dev \ 
    libgmp-dev \ 
    libgtk-3-dev \ 
    libhogweed? \ 
    libidn11-dev \ 
    libidn2-0-dev \ 
    libp11-kit-dev \ 
    libp11-kit0-dbg \ 
    libpthread-stubs0-dev \ 
    libsctp-dev \ 
    libsctp1 \ 
    libssl-dev \ 
    libtasn1-6-dbg \ 
    libtasn1-6-dev \ 
    libtool \ 
    libtspi-dev \ 
    libtspi1 \ 
    libxml2 \ 
    libxml2-dev \ 
    mscgen \ 
    openssl \ 
    phpmyadmin \ 
    pkg-config \ 
    python \ 
    python-dev \ 
    python-pexpect \ 
    subversion \ 
    tshark \ 
    unzip \ 
    vlan \ 
    wget 
ADD ./openair-cn /openair-cn
WORKDIR /openair-cn/SCRIPTS
RUN git checkout develop
RUN ./build_mme -i --force
RUN ./build_hss -i --force
RUN ./build_spgw -i --force


RUN ./check_hss_s6a_certificate /usr/local/etc/oai/freeDiameter/ hss.openair4G.eur
RUN ./check_mme_s6a_certificate /usr/local/etc/oai/freeDiameter/ mme.openair4G.eur
RUN ./build_hss -c
RUN ./build_mme -c
RUN ./build_spgw -c

RUN apt-get install -yq iptables 
ADD ./conf /usr/local/etc/oai

