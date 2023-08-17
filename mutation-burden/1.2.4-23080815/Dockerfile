# Stage 1: Build Stage
FROM rocker/r-ver:4.1.2 as build

ARG PYTHON_VER=3.8.13
ARG HTSLIB_VER=1.14
ARG SAMTOOLS_VER=1.16.1
ARG BCFTOOLS_VER=1.16
ARG BAMTOOLS_VER=2.5.1
ARG BEDTOOLS_VER=2.29.0

# Install Dependencies
RUN apt-get update -y && apt-get upgrade -y && apt-get install -y \
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
    curl \
    tabix

# Install HTSlib
RUN wget https://github.com/samtools/htslib/releases/download/${HTSLIB_VER}/htslib-${HTSLIB_VER}.tar.bz2 && \
    tar jxf htslib-${HTSLIB_VER}.tar.bz2 && \
    cd htslib-${HTSLIB_VER} && ./configure && make && make install && \
    cd / && \
    rm htslib-${HTSLIB_VER}.tar.bz2 && \
    rm -rf htslib-${HTSLIB_VER}

# Install Python 3.8.13
RUN wget https://www.python.org/ftp/python/${PYTHON_VER}/Python-${PYTHON_VER}.tgz &&\
    tar xzf Python-${PYTHON_VER}.tgz &&\
    cd Python-${PYTHON_VER} &&\
    ./configure --enable-optimizations &&\
    make altinstall &&\
    cd .. &&\
    rm -rf Python-${PYTHON_VER}.tgz &&\
    update-alternatives --install /usr/local/bin/python python /usr/local/bin/python3.8 1 &&\
    update-alternatives --install /usr/local/bin/pip pip /usr/local/bin/pip3.8 1 &&\
    pip install --upgrade pip

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
    cd / &&\
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
    cd / &&\
    rm -rf bamtools-${BAMTOOLS_VER}

# Stage 2: Final Stage
FROM rocker/r-ver:4.1.2
ENV PATH=/tgen_mutation_burden-1.2.4:$PATH
ARG MUTATION_BURDEN_VER=1.2.4

# Set labels for metadata
LABEL org.opencontainers.image.title="tgen_mutation_burden"
LABEL org.opencontainers.image.version="1.2.4"
LABEL org.opencontainers.image.description="This tool calculates the << Mutation Burden per Million Base >> of a Patient's Tumor"
LABEL org.opencontainers.image.url="https://github.com/tgen/tgen_mutation_burden"
LABEL org.opencontainers.image.licenses="https://github.com/tgen/tgen_mutation_burden/blob/master/LICENSE"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"

# Copy Applications from the Build Stage to the final image
COPY --from=build /usr/local/ /usr/local
COPY tgen_mutation_burden-1.2.4.tar.gz /
COPY module_install.sh /
COPY req_modules.csv /

# Install Required Packages and Clean Cache
RUN apt-get update -y && apt-get install --no-install-recommends -y \
    libcurl3-gnutls \
    libgsl23 \
    libjsoncpp1 \
    curl \
    tabix \
    wget \
    parallel \
    bc \
    tar && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean

# Configure Python 3.8.13
RUN update-alternatives --install /usr/local/bin/python python /usr/local/bin/python3.8 1 &&\
    update-alternatives --install /usr/local/bin/pip pip /usr/local/bin/pip3.8 1 &&\
    pip install --upgrade pip

# Configure and Run Script
RUN chmod +x module_install.sh && \
    ./module_install.sh && \
    rm module_install.sh && \
    rm req_modules.csv

# Download and install tgen_mutation_burden
RUN tar zxf tgen_mutation_burden-${MUTATION_BURDEN_VER}.tar.gz &&\
    rm tgen_mutation_burden-${MUTATION_BURDEN_VER}.tar.gz &&\
    cd tgen_mutation_burden-${MUTATION_BURDEN_VER} &&\
    chmod 755 tgen_mutation_burden.sh

# Create Working Directory
WORKDIR /data