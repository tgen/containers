# Stage 1: Build Stage
FROM rocker/r-ver:4.1.2 as build

# Environment Variables
ENV LD_LIBRARY_PATH=/usr/local/lib/:$LD_LIBRARY_PATH
ENV SRC /data

ARG PYTHON_VER=3.8.13
ARG HTSLIB_VER=1.14
ARG SAMTOOLS_VER=1.10
ARG BCFTOOLS_VER=1.10.2
ARG BEDTOOLS_VER=2.29.0
ARG BAMTOOLS_VER=2.5.1
ARG VT_VER=0.57721
ARG VCFMERGER_VER=0.9.4

# Install Dependencies
RUN apt-get update -y && apt-get upgrade -y && apt-get install --no-install-recommends -y \
    perl \
    gcc \
    libncurses5-dev \
    libbz2-dev \
    liblzma-dev \
    libcurl4-gnutls-dev \
    libssl-dev \
    wget \
    tar \
    ca-certificates \
    bzip2 \
    autoconf \
    automake \
    make \
    gcc \
    libperl-dev \
    libgsl0-dev \
    cmake \
    g++ \
    libjsoncpp-dev \
    pkg-config \
    zlib1g-dev \
    libdata-dumper-simple-perl \
    build-essential \ 
    checkinstall \
    libreadline-gplv2-dev \ 
    libncursesw5-dev \ 
    libsqlite3-dev \ 
    tk-dev \ 
    libgdbm-dev \ 
    libc6-dev \ 
    libbz2-dev \ 
    libffi-dev \
    tabix \
    git \
    vim-common \
    fonts-freefont-ttf \
    openjdk-11-jdk && \
    # Move FreeSansBold to the path expected by vcfMerger2
    mkdir /usr/share/fonts/gnu-free && \
    mv /usr/share/fonts/truetype/freefont/FreeSansBold.ttf /usr/share/fonts/gnu-free/

WORKDIR $SRC

# Install Python 3.8.13
RUN wget https://www.python.org/ftp/python/${PYTHON_VER}/Python-${PYTHON_VER}.tgz &&\
    tar xzf Python-${PYTHON_VER}.tgz &&\
    cd Python-${PYTHON_VER} &&\
    ./configure --enable-optimizations &&\
    make altinstall &&\
    cd .. &&\
    rm -rf Python-${PYTHON_VER}.tgz &&\
    update-alternatives --install /usr/local/bin/python python /usr/local/bin/python3.8 1 &&\
    update-alternatives --install /usr/local/bin/python3 python3 /usr/local/bin/python3.8 2 &&\
    update-alternatives --install /usr/local/bin/pip pip /usr/local/bin/pip3.8 1 &&\
    python3.8 -m pip install --upgrade pip

# Install HTSlib
RUN wget https://github.com/samtools/htslib/releases/download/${HTSLIB_VER}/htslib-${HTSLIB_VER}.tar.bz2 && \
    tar jxf htslib-${HTSLIB_VER}.tar.bz2 && \
    cd htslib-${HTSLIB_VER} && ./configure && make && make install && \
    cd .. && \
    rm htslib-${HTSLIB_VER}.tar.bz2 && \
    rm -rf htslib-${HTSLIB_VER}

# Install Samtools
RUN wget https://github.com/samtools/samtools/releases/download/${SAMTOOLS_VER}/samtools-${SAMTOOLS_VER}.tar.bz2 && \
    tar jxf samtools-${SAMTOOLS_VER}.tar.bz2 && \
    rm samtools-${SAMTOOLS_VER}.tar.bz2 && \
    cd samtools-${SAMTOOLS_VER} && \
    ./configure && \
    make && \
    make install

# Install Bcftools
RUN wget https://github.com/samtools/bcftools/releases/download/${BCFTOOLS_VER}/bcftools-${BCFTOOLS_VER}.tar.bz2 && \
    tar jxf bcftools-${BCFTOOLS_VER}.tar.bz2 && \
    cd bcftools-${BCFTOOLS_VER} && \
    ./configure --enable-libgsl && \
    make && \
    make install && \
    cd .. && \
    rm bcftools-${BCFTOOLS_VER}.tar.bz2 && \
    rm -rf bcftools-${BCFTOOLS_VER}

# Install BedTools
RUN wget https://github.com/arq5x/bedtools2/archive/v${BEDTOOLS_VER}.tar.gz -q --show-progress &&\
    tar -zxf v${BEDTOOLS_VER}.tar.gz &&\
    rm v${BEDTOOLS_VER}.tar.gz &&\
    cd bedtools2-${BEDTOOLS_VER} &&\
    make &&\
    cp bin/* /usr/local/bin &&\
    cd .. &&\
    rm -rf bedtools2-${BEDTOOLS_VER}

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
    cd ../.. &&\
    rm -rf bamtools-${BAMTOOLS_VER}

# Install vt
RUN wget https://github.com/atks/vt/archive/refs/tags/${VT_VER}.tar.gz -q --show-progress && \
    tar zxf ${VT_VER}.tar.gz && \
    cd vt-${VT_VER} && \
    make && \
    mv vt /usr/local/bin && \
    cd .. && rm ${VT_VER}.tar.gz && \
    rm -rf vt-${VT_VER}

# Install Python2.7
RUN wget https://www.python.org/ftp/python/2.7.18/Python-2.7.18.tgz &&\
    tar xzf Python-2.7.18.tgz &&\
    rm -rf Python-2.7.18.tgz &&\
    cd Python-2.7.18 &&\
    ./configure --enable-optimizations &&\
    make altinstall &&\
    wget https://bootstrap.pypa.io/pip/2.7/get-pip.py &&\
    python2.7 get-pip.py

# Install Phaser Python Dependencies
RUN python2.7 -m pip install Cython==0.28.1 numpy==1.16.6 pysam==0.20.0 scipy==1.2.3  &&\    
    update-alternatives --install /usr/local/bin/python2 python2 /usr/local/bin/python2.7 1

# Install phASER
RUN git clone https://github.com/secastel/phaser.git && \
    cd phaser/phaser && \
    python2 setup.py build_ext --inplace && \
    chmod +x phaser.py && \
    sed -i 's/\#\!\/home\/bin\/python2/\#\!\/usr\/bin\/env python2/' phaser.py
# python2.7 phaser/phaser/phaser.py or 

# Install vcfMerger2 Dependencies
RUN python3.8 -m pip install Cython==0.29.33 cyvcf2==0.30.18 argparse==1.1 natsort==5.0.3 pybedtools==0.9.0 intervene==0.6.4 Pillow==9.4.0 --use-pep517
RUN Rscript -e 'install.packages("UpSetR")'

# Download and install vcfMerger2
RUN wget https://github.com/tgen/vcfMerger2/archive/refs/tags/v${VCFMERGER_VER}.tar.gz -q --show-progress && \
    tar zxf v${VCFMERGER_VER}.tar.gz && \
    mv vcfMerger2-${VCFMERGER_VER} vcfMerger2 && \
    rm v${VCFMERGER_VER}.tar.gz
# vcfMerger2.py --help

# Stage 2: Final Stage
FROM rocker/r-ver:4.1.2

ENV LD_LIBRARY_PATH=/usr/local/lib/:$LD_LIBRARY_PATH
ENV SRC /data
ENV PATH=${SRC}/vcfMerger2/bin:${SRC}/phaser/phaser:$PATH

# Set labels for metadata
LABEL org.opencontainers.image.title="vcfMerger2"
LABEL org.opencontainers.image.version="0.9.4"
LABEL org.opencontainers.image.description="vcfMerger2 is a tool merger for 2 to N somatic variants vcf files."
LABEL org.opencontainers.image.url="https://github.com/tgen/vcfMerger2"
LABEL org.opencontainers.image.licenses="https://github.com/tgen/vcfMerger2/blob/v0.9.4/LICENSE.md"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"

# Copy Applications from the Build Stage to the final image
COPY --from=build /usr/local/ /usr/local
COPY --from=build /usr/share/fonts/ /usr/share/fonts
COPY --from=build /data/ /data

# Install Required Packages and Clean Cache
RUN apt-get update -y && apt-get upgrade -y && apt-get install --no-install-recommends  -y \
    libcurl3-gnutls \
    libgsl23 \
    libjsoncpp1 \
    gawk \
    xxd \
    openjdk-11-jdk &&\
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean

# Install Python 3.8.13
RUN update-alternatives --install /usr/local/bin/python python /usr/local/bin/python3.8 1 &&\
    update-alternatives --install /usr/local/bin/python3 python3 /usr/local/bin/python3.8 2 &&\
    update-alternatives --install /usr/local/bin/pip pip /usr/local/bin/pip3.8 1 &&\
    python3.8 -m pip install --upgrade pip

RUN update-alternatives --install /usr/local/bin/python2 python2 /usr/local/bin/python2.7 1

# Change default sh to bash instead of dash
RUN echo "dash dash/sh boolean false" | debconf-set-selections
RUN DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash

# Create Working Directory
WORKDIR /data