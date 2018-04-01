#
# Setup:
#
#  - gcc 6
#  - cmake 3.10.3
#  - unzip
#  - SDL2 dev
#  - bwapi: latest from OpenBW repository master
#  - openbw: latest from OpenBW repository master
#  - BW 1.16.1
#  - SSCAIT map pool
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

RUN apt-get install unzip

RUN cd home \ 
      && git clone https://github.com/OpenBW/bwapi.git \
      && git clone https://github.com/OpenBW/openbw.git

RUN cd /home/bwapi/ \
      && mkdir build \
      && cd build \
      && cmake .. -DCMAKE_BUILD_TYPE=Release -DOPENBW_DIR=../../openbw -DOPENBW_ENABLE_UI=1 \
      && make
 
RUN mkdir /home/tmp/ \
      && cd /home/tmp/ \
      && curl -SL 'http://files.theabyss.ru/sc/starcraft.zip' -o starcraft.zip \ 
      && unzip starcraft.zip \
      && mv patch_rt.mpq /home/bwapi/build/bin/Patch_rt.mpq \
      && mv BROODAT.MPQ /home/bwapi/build/bin/BrooDat.mpq \
      && mv STARDAT.MPQ /home/bwapi/build/bin/StarDat.mpq
      
RUN mkdir /home/bwapi/build/bin/bwapi-data \
      && cp /home/bwapi/bwapi.ini.example /home/bwapi/build/bin/bwapi-data/bwapi.ini
      
RUN cd /home/tmp/ \
      && curl -SL 'https://sscaitournament.com/files/sscai_map_pack.zip' -o maps.zip \
      && unzip maps.zip \
      && mkdir /home/bwapi/build/bin/maps \
      && mv sscai/* /home/bwapi/build/bin/maps
      
      