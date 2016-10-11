FROM ubuntu:14.04
RUN apt-get update
RUN apt-get install -yq git
ADD ./openairinterface5g /openairinterface5g
WORKDIR /openairinterface5g
RUN git checkout develop
ENV GIT_SSL_NO_VERIFY true
RUN . ./oaienv && cd cmake_targets && ./build_oai -w BLADERF -I --disable-hardware-dependency
