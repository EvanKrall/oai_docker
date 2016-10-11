FROM ubuntu:14.04
RUN apt-get update
RUN apt-get install -yq git
ADD ./openair-cn /openair-cn
WORKDIR /openair-cn/SCRIPTS
RUN git checkout develop
RUN ./build_mme -i --force
RUN ./build_hss -i --force
RUN ./build_spgw -i --force

