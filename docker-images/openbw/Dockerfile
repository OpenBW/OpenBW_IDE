#
# Setup:
#
#  - gcc 6
#  - cmake 3.10.3
#  - SDL2 dev
#  - bwapi: latest from OpenBW repository master
#  - openbw: latest from OpenBW repository master
#

FROM gcc:6

RUN apt-get update

RUN curl https://cmake.org/files/v3.10/cmake-3.10.3-Linux-x86_64.sh -o /tmp/curl-install.sh \
      && chmod u+x /tmp/curl-install.sh \
   	  && mkdir /usr/bin/cmake \
      && /tmp/curl-install.sh --skip-license --prefix=/usr/bin/cmake \
      && rm /tmp/curl-install.sh

ENV PATH="/usr/bin/cmake/bin:${PATH}"

RUN apt-get --assume-yes install libsdl2-dev

RUN cd home \ 
      && git clone https://github.com/OpenBW/bwapi.git \
      && git clone https://github.com/OpenBW/openbw.git

RUN cd /home/bwapi/ \
      && mkdir build \
      && cd build \
      && cmake .. -DCMAKE_BUILD_TYPE=Release -DOPENBW_DIR=../../openbw -DOPENBW_ENABLE_UI=1 \
      && make
      