FROM ubuntu:14.04
RUN apt-get update
RUN apt-get install -yq git
RUN apt-get install -y libtasn1-3-dev autoconf automake bison build-essential cmake cmake-curses-gui doxygen doxygen-gui texlive-latex-base ethtool flex gccxml gdb git graphviz gtkwave guile-2.0-dev iperf iproute iptables iptables-dev libatlas-base-dev libatlas-dev libblas-dev libconfig8-dev libffi-dev libforms-bin libforms-dev libgcrypt11-dev libgmp-dev libgtk-3-dev libidn2-0-dev libidn11-dev libmysqlclient-dev liboctave-dev libpgm-dev libpython2.7-dev libsctp1 libsctp-dev libssl-dev libtool libusb-1.0-0-dev libxml2 libxml2-dev libxslt1-dev mscgen octave octave-signal openssh-client openssh-server openssl python subversion xmlstarlet python-pip pydb wget
ADD ./openairinterface5g /openairinterface5g
WORKDIR /openairinterface5g
RUN git checkout develop
ENV GIT_SSL_NO_VERIFY true
ARG radio
RUN if [ $radio = LMSSDR ]; then \
    echo 'deb http://ppa.launchpad.net/myriadrf/drivers/ubuntu trusty main' > /etc/apt/sources.list.d/myriadrf.list &&\
    apt-key adv --keyserver keyserver.ubuntu.com --recv-key 22C627172ECB91FE &&\
    apt-get update &&\
    apt-get install -yq limesuite limesuite-udev soapysdr soapysdr-module-lms7 liblimesuite-dev;\
  fi # bump1
RUN . ./oaienv && cd cmake_targets && ./build_oai -w $radio -I --disable-hardware-dependency
RUN . ./oaienv && cd cmake_targets && ./build_oai -w $radio -x -c --eNB

ADD enb.band7.tm1.lmssdr.conf ./

CMD . ./oaienv && cd cmake_targets/lte_build_oai/build && ./lte-softmodem -O /openairinterface5g/enb.band7.tm1.lmssdr.conf --rf-config-file $OPENAIR_DIR/targets/ARCH/LMSSDR/LimeSDR.ini
