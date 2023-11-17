FROM python:3.8.13-slim-bullseye as build
ARG BEDTOOLS_VER=2.29.0
ARG BAMTOOLS_VER=2.5.1
ARG SAMTOOLS_VER=1.16.1
#________________________________
# Install Dependencies
RUN apt-get update && apt-get install --no-install-recommends -y \
    perl \
    automake \
    autoconf \
    wget \
    ca-certificates \
    tar \
    bzip2 \
    make \
    gcc \
    zlib1g-dev \
    libncurses5-dev \
    libbz2-dev \
    liblzma-dev \
    libcurl4-gnutls-dev \
    libssl-dev \
    cmake \
    g++ \
    libjsoncpp-dev \
    pkg-config
# Install Samtools
RUN wget https://github.com/samtools/samtools/releases/download/${SAMTOOLS_VER}/samtools-${SAMTOOLS_VER}.tar.bz2 && \
    tar jxf samtools-${SAMTOOLS_VER}.tar.bz2 && \
    rm samtools-${SAMTOOLS_VER}.tar.bz2 && \
    cd samtools-${SAMTOOLS_VER} && \
    ./configure && \
    make && \
    make install
#________________________________
# Install BedTools
RUN wget https://github.com/arq5x/bedtools2/archive/v${BEDTOOLS_VER}.tar.gz -q --show-progress &&\
    tar -zxf v${BEDTOOLS_VER}.tar.gz &&\
    rm v${BEDTOOLS_VER}.tar.gz &&\
    cd bedtools2-${BEDTOOLS_VER} &&\
    make &&\
    cp bin/* /usr/local/bin &&\
    cd / &&\
    rm -rf bedtools2-${BEDTOOLS_VER}
#________________________________
# Install BamTools
RUN wget https://github.com/pezmaster31/bamtools/archive/v${BAMTOOLS_VER}.tar.gz -q --show-progress &&\
    tar -zxf v${BAMTOOLS_VER}.tar.gz &&\
    rm v${BAMTOOLS_VER}.tar.gz &&\
    cd bamtools-${BAMTOOLS_VER} &&\
    mkdir build &&\
    cd build &&\
    cmake -DCMAKE_INSTALL_PREFIX=/usr/local .. &&\
    make &&\
    make install &&\
    cd / &&\
    rm -rf bamtools-${BAMTOOLS_VER}
#________________________________
# Starting 2nd Stage
FROM python:3.8.13-slim-bullseye
#________________________________
# Copy Applications from 1st Build Stage
COPY --from=build /usr/local/ /usr/local
#________________________________
# Install Required Packages and Clean Cache
RUN apt-get update && apt-get install --no-install-recommends -y \
    gcc \
    zlib1g-dev \
    libbz2-dev \
    liblzma-dev \
    make \
    libncursesw6 \
    libcurl3-gnutls \
    libjsoncpp24 && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean
# Upgrade pip and install required packages
RUN pip install --no-compile --no-cache-dir --upgrade pip && \
    pip install --no-compile --no-cache-dir --upgrade wheel && \
    pip install --no-compile --no-cache-dir pandas numpy && \
    pip install --no-compile --no-cache-dir pod5