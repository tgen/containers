FROM debian:bullseye-20230208-slim as build
ARG SAMTOOLS_VER=1.16.1

# Install Samtools Dependencies
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
    libssl-dev

# Install Samtools
RUN wget https://github.com/samtools/samtools/releases/download/${SAMTOOLS_VER}/samtools-${SAMTOOLS_VER}.tar.bz2 && \
    tar jxf samtools-${SAMTOOLS_VER}.tar.bz2 && \
    rm samtools-${SAMTOOLS_VER}.tar.bz2 && \
    cd samtools-${SAMTOOLS_VER} && \
    ./configure && \
    make && \
    make install

# Starting 2nd Stage
FROM debian:bullseye-20230208-slim

# Copy Samtools Application from 1st Build Stage
COPY --from=build /usr/local/ /usr/local

# Install Samtools Required Packages and Clean Cache
RUN apt-get update && apt-get install --no-install-recommends -y \
    libncursesw6 \
    libcurl3-gnutls && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean

# Create Working Directory
WORKDIR /data