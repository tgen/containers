# Stage 1: Build Stage
FROM debian:bullseye-20230208-slim as build
ARG MSISENSOR_VER=1.1.a
ARG SAMTOOLS_VER=1.10

# Install Dependencies
RUN apt-get update -y && apt-get upgrade -y && apt-get install -y \
    ca-certificates \
    wget \
    tar \
    bzip2 \
    make \
    gcc \
    zlib1g-dev \
    libncurses-dev \
    libbz2-dev \
    liblzma-dev \
    libcurl4-gnutls-dev \
    libssl-dev

# Download and install SAMtools
RUN wget https://github.com/samtools/samtools/releases/download/${SAMTOOLS_VER}/samtools-${SAMTOOLS_VER}.tar.bz2 &&\
    tar jxf samtools-${SAMTOOLS_VER}.tar.bz2 &&\
    rm samtools-${SAMTOOLS_VER}.tar.bz2 &&\
    cd samtools-${SAMTOOLS_VER} &&\
    ./configure &&\
    make &&\
    make install &&\
    cd / &&\
    rm -rf samtools-${SAMTOOLS_VER}

# Copy of MSIsensor tarball
COPY ${MSISENSOR_VER}.tar.gz /

# Install MSISensor
RUN tar zxf ${MSISENSOR_VER}.tar.gz &&\
    cp msisensor-pro-${MSISENSOR_VER}/binary/msisensor-pro /usr/local/sbin &&\
    rm ${MSISENSOR_VER}.tar.gz &&\
    rm -rf msisensor-pro-${MSISENSOR_VER}

# Stage 2: Final Stage
FROM debian:bullseye-20230208-slim

# Set labels for metadata
LABEL org.opencontainers.image.title="MSISensor"
LABEL org.opencontainers.image.version="1.1.a"
LABEL org.opencontainers.image.description="MSIsensor-pro is an updated version of msisensor. MSIsensor-pro evaluates Microsatellite Instability (MSI) for cancer patients with next generation sequencing data. It accepts the whole genome sequencing, whole exome sequencing and target region (panel) sequencing data as input."
LABEL org.opencontainers.image.citation="Peng Jia, Xiaofei Yang, Li Guo, Bowen Liu, Jiadong Lin, Hao Liang, et al. MSIsensor-pro: fast, accurate, and matched-normal-sample-free detection of microsatellite instability. Genomics Proteomics Bioinformatics 2020,18(1)."
LABEL org.opencontainers.image.url="https://github.com/xjtu-omics/msisensor-pro"
LABEL org.opencontainers.image.licenses="https://github.com/xjtu-omics/msisensor-pro/blob/master/LICENSE"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"

# Copy MSISensor/Samtools Application from the Build Stage to the final image
COPY --from=build /usr/local/ /usr/local

# Install Required Packages and Clean Cache
RUN apt-get update -y && apt-get upgrade -y && apt-get install --no-install-recommends -y \
    gcc \
    libncursesw6 \
    libcurl3-gnutls &&\
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean

# Create Working Directory
WORKDIR /data