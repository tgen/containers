# Stage 1: Build Stage
FROM debian:bullseye-20230208-slim as build
ARG BWA_MEM2_VER=2.2.1
ARG SAMTOOLS_VER=1.17

# Install Dependencies
RUN apt-get update && apt-get install -y \
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
    libbz2-dev \
    liblzma-dev \
    libcurl4-gnutls-dev \
    libssl-dev \ 
    libncurses5-dev

# Install Samtools
RUN wget https://github.com/samtools/samtools/releases/download/${SAMTOOLS_VER}/samtools-${SAMTOOLS_VER}.tar.bz2 && \
    tar jxf samtools-${SAMTOOLS_VER}.tar.bz2 && \
    rm samtools-${SAMTOOLS_VER}.tar.bz2 && \
    cd samtools-${SAMTOOLS_VER} && \
    ./configure && \
    make && \
    make install

# Install Bwa-Mem2
RUN wget https://github.com/bwa-mem2/bwa-mem2/releases/download/v${BWA_MEM2_VER}/bwa-mem2-${BWA_MEM2_VER}_x64-linux.tar.bz2 && \
    tar jxf bwa-mem2-${BWA_MEM2_VER}_x64-linux.tar.bz2 && \
    rm bwa-mem2-${BWA_MEM2_VER}_x64-linux.tar.bz2 && \
    mv bwa-mem2-${BWA_MEM2_VER}_x64-linux bwa-mem2 && \
    mv /bwa-mem2/bwa* /usr/local/bin/

# Stage 2: Final Stage
FROM debian:bullseye-20230208-slim
ARG FGBIO_VER=2.0.2

# Set labels for metadata
LABEL org.opencontainers.image.title="Fgbio"
LABEL org.opencontainers.image.version="2.0.2"
LABEL org.opencontainers.image.description="Fgbio is a set of command line tools to perform bioinformatic/genomic data analysis. The collection of tools within fgbio are used by our customers and others both for ad-hoc data analysis and within production pipelines."
LABEL org.opencontainers.image.url="https://github.com/fulcrumgenomics/fgbio"
LABEL org.opencontainers.image.licenses="https://github.com/fulcrumgenomics/fgbio/blob/2.0.2/LICENSE"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided  “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"

# Copy Bwa-Mem2/Samtools Application from the Build Stage to the final image
COPY --from=build /usr/local/ /usr/local

# Install Bwa-Mem2/Samtools Required Packages and Clean Cache
RUN apt-get update && apt-get install --no-install-recommends -y \
    libcurl3-gnutls \
    libncursesw6 \
    software-properties-common \
    apt-transport-https \
    gnupg2 \
    wget \
    ca-certificates && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean

RUN wget -qO - https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public |  apt-key add - &&\
    add-apt-repository --yes https://adoptopenjdk.jfrog.io/adoptopenjdk/deb/ &&\
    apt-get update -y && apt-get install -y adoptopenjdk-8-hotspot

# Install Fgbio
RUN wget "https://github.com/fulcrumgenomics/fgbio/releases/download/${FGBIO_VER}/fgbio-${FGBIO_VER}.jar" &&\
    cd /usr/bin &&\
    printf "#!/bin/bash\nexec java -jar /data/fgbio-${FGBIO_VER}.jar \$@\n" >> fgbio &&\
    chmod +x fgbio