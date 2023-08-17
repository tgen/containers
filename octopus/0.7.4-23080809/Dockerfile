# Stage 1: Build Stage
FROM python:3.7.16-slim-bullseye as build
ARG HTSLIB_VER=1.17
ARG OCTOPUS_VER=0.7.4
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib/

RUN apt-mark hold tzdata && apt update && apt upgrade -y && apt install --no-install-recommends -y \
    wget \
    bzip2 \
    libbz2-dev \
    zlib1g-dev \
    libcurl4-gnutls-dev \
    xz-utils \
    liblzma-dev \
    libssl-dev \
    curl \
    gcc \
    make \
    git \
    cmake \
    g++ \
    libboost-all-dev \
    libgmp-dev && \

# Install HSTlib.  Required for Octopus and pysam python module.
    wget https://github.com/samtools/htslib/releases/download/${HTSLIB_VER}/htslib-${HTSLIB_VER}.tar.bz2 && \
    tar jxf htslib-${HTSLIB_VER}.tar.bz2 && \
    cd htslib-${HTSLIB_VER} && \
    ./configure && \
    make && \
    make install && \
    cd / && \

# Install octopus
    pip install distro && \
    wget https://github.com/luntergroup/octopus/archive/v${OCTOPUS_VER}.tar.gz && \
    tar xf v${OCTOPUS_VER}.tar.gz && \
    octopus-${OCTOPUS_VER}/scripts/install.py --threads 4 && \
    cd / && \
    mv octopus-${OCTOPUS_VER} octopus

# Stage 2: Final Stage
FROM python:3.7.16-slim-bullseye
ARG BOOST_VER=1.74.0
ENV LD_LIBRARY_PATH=/usr/local/lib/
ENV PATH=/octopus/bin:$PATH

# Set labels for metadata
LABEL org.opencontainers.image.title="octopus"
LABEL org.opencontainers.image.version="0.7.4"
LABEL org.opencontainers.image.description="Octopus is a mapping-based variant caller that implements several calling models within a unified haplotype-aware framework."
LABEL org.opencontainers.image.url="https://github.com/luntergroup/octopus"
LABEL org.opencontainers.image.licenses="https://github.com/luntergroup/octopus/blob/v0.7.4/LICENSE"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"

# Copy Octopus Application from the Build Stage to the final image
COPY --from=build /usr/local/ /usr/local
COPY --from=build /octopus /octopus

# Install Required Packages and Clean Cache
RUN apt-mark hold tzdata && apt update && apt upgrade -y && apt-get install --no-install-recommends -y \
    libbz2-1.0 \
    zlib1g \
    libcurl3-gnutls \
    xz-utils \
    liblzma5 \
    libssl1.1 \
    libboost-atomic${BOOST_VER} \
    libboost-chrono${BOOST_VER} \
    libboost-container${BOOST_VER} \
    libboost-context${BOOST_VER} \
    libboost-coroutine${BOOST_VER} \
    libboost-date-time${BOOST_VER} \
    libboost-fiber${BOOST_VER} \
    libboost-filesystem${BOOST_VER} \
    libboost-graph-parallel${BOOST_VER} \
    libboost-graph${BOOST_VER} \
    libboost-iostreams${BOOST_VER} \
    libboost-locale${BOOST_VER} \
    libboost-log${BOOST_VER} \
    libboost-math${BOOST_VER} \
    libboost-mpi-python${BOOST_VER} \
    libboost-mpi${BOOST_VER} \
    libboost-nowide${BOOST_VER} \
    libboost-numpy${BOOST_VER} \
    libboost-program-options${BOOST_VER} \
    libboost-python${BOOST_VER} \
    libboost-random${BOOST_VER} \
    libboost-regex${BOOST_VER} \
    libboost-serialization${BOOST_VER} \
    libboost-stacktrace${BOOST_VER} \
    libboost-system${BOOST_VER} \
    libboost-test${BOOST_VER} \
    libboost-thread${BOOST_VER} \
    libboost-timer${BOOST_VER} \
    libboost-type-erasure${BOOST_VER} \
    libboost-wave${BOOST_VER} \
    libgmp10