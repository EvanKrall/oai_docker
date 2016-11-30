FROM ubuntu:14.04
RUN apt-get update
RUN apt-get install -yq git
RUN apt-get install -y libtasn1-3-dev autoconf automake bison build-essential cmake cmake-curses-gui doxygen doxygen-gui texlive-latex-base ethtool flex gccxml gdb git graphviz gtkwave guile-2.0-dev iperf iproute iptables iptables-dev libatlas-base-dev libatlas-dev libblas-dev libconfig8-dev libffi-dev libforms-bin libforms-dev libgcrypt11-dev libgmp-dev libgtk-3-dev libidn2-0-dev libidn11-dev libmysqlclient-dev liboctave-dev libpgm-dev libpython2.7-dev libsctp1 libsctp-dev libssl-dev libtool libusb-1.0-0-dev libxml2 libxml2-dev libxslt1-dev mscgen octave octave-signal openssh-client openssh-server openssl python subversion xmlstarlet python-pip pydb wget
ADD ./openairinterface5g /openairinterface5g
WORKDIR /openairinterface5g
RUN git checkout develop
ENV GIT_SSL_NO_VERIFY true
RUN . ./oaienv && cd cmake_targets && ./build_oai -w BLADERF -I --disable-hardware-dependency
RUN . ./oaienv && cd cmake_targets && ./build_oai -w BLADERF -x -c --eNB

ADD enb.band7.tm1.bladerfx40.conf ./

CMD . ./oaienv && cd cmake_targets/lte_build_oai/build && ./lte-softmodem -O $OPENAIR_DIR/targets/PROJECTS/GENERIC-LTE-EPC/CONF/enb.band7.tm1.bladerfx40.conf
