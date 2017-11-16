FROM ubuntu:16.04
RUN apt-get update && apt-get install -yq --no-install-recommends pcscd pcsc-tools libccid libpcsclite-dev

RUN apt-get -yq install python-pip swig python-dev git
RUN pip install pyscard
WORKDIR /root
RUN git clone http://git.osmocom.org/pysim/
WORKDIR /root/pysim

