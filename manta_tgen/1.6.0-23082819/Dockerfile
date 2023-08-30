FROM debian:bullseye-20230208-slim as build

ARG MANTA_VER=1.6.0
ARG HTSLIB_VER=1.17

# Install Dependencies
RUN apt-get update -y && apt-get install --no-install-recommends -y \
    wget \
    autoconf \
    automake \
    make \
    patch \
    gcc \
    g++ \
    perl \
    python2 \
    ca-certificates \
    zlib1g-dev \
    libbz2-dev \
    liblzma-dev \
    libcurl4-gnutls-dev \
    bzip2 \
    libssl-dev

# Install manta and apply a patch to mantaWorkflow.py
RUN wget -qO- https://github.com/Illumina/manta/releases/download/v${MANTA_VER}/manta-${MANTA_VER}.release_src.tar.bz2 | tar -xjf - && \
    wget -qO- https://github.com/tgen/manta/commit/d88d22e18eb60790f5e828cf1d6e074e03a43055.patch | patch manta-${MANTA_VER}.release_src/src/python/lib/mantaWorkflow.py - && \
    mkdir build && cd build && \
    ../manta-${MANTA_VER}.release_src/configure --prefix=/usr/local && \
    make && \
    make install

# Install htslib
RUN wget https://github.com/samtools/htslib/releases/download/${HTSLIB_VER}/htslib-${HTSLIB_VER}.tar.bz2 && \
    tar jxf htslib-${HTSLIB_VER}.tar.bz2 && \
    cd htslib-${HTSLIB_VER} && \
    ./configure && \
    make && \
    make install

# Starting 2nd Stage
FROM debian:bullseye-20230208-slim

# Set labels for metadata
LABEL org.opencontainers.image.title="manta"
LABEL org.opencontainers.image.version="1.6.0"
LABEL org.opencontainers.image.description="Manta calls structural variants (SVs) and indels from mapped paired-end sequencing reads."
LABEL org.opencontainers.image.citation="Chen, X. et al. (2016) Manta: rapid detection of structural variants and indels for germline and cancer sequencing applications. Bioinformatics, 32, 1220-1222. doi:10.1093/bioinformatics/btv710"
LABEL org.opencontainers.image.url="https://github.com/tgen/manta"
LABEL org.opencontainers.image.licenses="https://github.com/tgen/manta/blob/v1.6.0/LICENSE.txt"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"


# Copy <> Application from 1st Build Stage
COPY --from=build /usr/local/ /usr/local

RUN apt-get update -y && apt-get install --no-install-recommends -y \
    libcurl3-gnutls \
    libgsl25 \
    python2 && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean
