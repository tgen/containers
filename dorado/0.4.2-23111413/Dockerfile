FROM debian:bullseye-20230208-slim as build
ARG DORADO_VER=0.4.2

# Install Dependencies
RUN apt-get update -y && apt-get install -y \
	curl \
	git \
	build-essential \
    ca-certificates \
    libhdf5-dev \
    libssl-dev \
    libzstd-dev \
    wget

# Install Dorado
RUN wget -qO- https://cdn.oxfordnanoportal.com/software/analysis/dorado-${DORADO_VER}-linux-x64.tar.gz |\
    tar -xzf -
RUN cp -R dorado-${DORADO_VER}*/bin/* /usr/local/bin &&\
    cp -R dorado-${DORADO_VER}*/lib/* /usr/local/lib

# Starting 2nd Stage
FROM debian:bullseye-20230208-slim

# Copy Dorado Application from 1st Build Stage
COPY --from=build /usr/local/ /usr/local

# Install Required Packages and Clean Cache
RUN apt-get update -y && apt-get install -y \
    ca-certificates \
    curl && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean

# Create Working Directory
WORKDIR /data