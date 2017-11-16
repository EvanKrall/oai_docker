FROM ubuntu:14.04
ARG radio
RUN apt-get update
RUN apt-get install -yq \
  git \
  libtasn1-3-dev \
  autoconf \
  automake \
  bison \
  build-essential \
  cmake \
  cmake-curses-gui \
  doxygen \
  doxygen-gui \
  texlive-latex-base \
  ethtool \
  flex \
  gccxml \
  gdb \
  git \
  graphviz \
  gtkwave \
  guile-2.0-dev \
  iperf \
  iproute \
  iptables \
  iptables-dev \
  libatlas-base-dev \
  libatlas-dev \
  libblas-dev \
  libconfig8-dev \
  libffi-dev \
  libforms-bin \
  libforms-dev \
  libgmp-dev \
  libgtk-3-dev \
  libidn2-0-dev \
  libidn11-dev \
  libmysqlclient-dev \
  liboctave-dev \
  libpgm-dev \
  libsctp1 \
  libsctp-dev \
  libssl-dev \
  libtool \
  libusb-1.0-0-dev \
  libxml2 \
  libxml2-dev \
  mscgen \
  octave \
  octave-signal \
  openssl \
  python \
  subversion \
  xmlstarlet \
  python-pip \
  pydb \
  wget
RUN if [ $radio = LMSSDR ]; then \
    echo 'deb http://ppa.launchpad.net/myriadrf/drivers/ubuntu trusty main' > /etc/apt/sources.list.d/myriadrf.list &&\
    apt-key adv --keyserver keyserver.ubuntu.com --recv-key 22C627172ECB91FE &&\
    apt-get update &&\
    apt-get install -yq limesuite limesuite-udev soapysdr soapysdr-module-lms7 liblimesuite-dev;\
    ln -s /usr/include/lime /usr/local/include/lime;\
  fi # bump1
ADD ./openairinterface5g /openairinterface5g
WORKDIR /openairinterface5g
RUN . ./oaienv && cd cmake_targets && ./build_oai -w $radio -I --disable-hardware-dependency ; retval=$?; cat /openairinterface5g/cmake_targets/log/* || true; exit $retval
ARG target
#RUN if [ $target = UE ]; then \
#    echo 'deb http://ppa.launchpad.net/ubuntu-toolchain-r/test/ubuntu trusty main' > /etc/apt/sources.list.d/ubuntu-toolchain-r-test.list &&\
#    apt-key adv --keyserver keyserver.ubuntu.com --recv-key 1E9377A2BA9EF27F &&\
#    apt-get update &&\
#    apt-get install -yq gcc-4.9 g++-4.9 &&\
#    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 1 --slave /usr/bin/g++ g++ /usr/bin/g++-4.9 ;\
#  fi
#RUN if [ $target = UE ]; then \
#    echo 'deb http://us.archive.ubuntu.com/ubuntu/ xenial-updates main' > /etc/apt/sources.list.d/xenial-updates.list &&\
#    apt-get update &&\
#    apt-get install -yq linux-headers-$(uname -r);\
#  fi
RUN . ./oaienv && cd cmake_targets && ./build_oai -I -w $radio -c --$target --disable-hardware-dependency; retval=$?; cat /openairinterface5g/cmake_targets/log/* || true; exit $retval

WORKDIR /openairinterface5g/cmake_targets/lte_build_oai/build
