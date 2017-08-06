FROM ubuntu:16.04
RUN echo 'deb http://ppa.launchpad.net/bladerf/bladerf/ubuntu xenial main' > /etc/apt/sources.list.d/bladerf.list && apt-key adv --keyserver keyserver.ubuntu.com --recv-key BE99746B2FB21B35
RUN apt-get update && apt-get install -yq --no-install-recommends cmake build-essential libfftw3-dev libncurses5-dev libblas-dev libboost-dev liblapack-dev libboost-thread-dev libboost-system-dev libhackrf-dev libbladerf-dev
ADD https://downloads.sourceforge.net/project/itpp/itpp/4.3.1/itpp-4.3.1.tar.bz2 /itpp.tar.bz2
RUN tar -axvf /itpp.tar.bz2
RUN cd /itpp-4.3.1 && mkdir build && cd build && cmake .. && make && make install
RUN ldconfig
ADD LTE-Cell-Scanner /lcs
WORKDIR /lcs
RUN mkdir build
WORKDIR build
RUN cmake ../ -DUSE_HACKRF=1
RUN make
RUN make install
