# Stage 1: Build Stage
FROM python:3.8.13-slim-bullseye as build
ARG HTSLIB_VER=1.14
ARG BCFTOOLS_VER=1.10.2

# Install Dependencies
RUN apt-get update -y && apt-get upgrade -y && apt-get install -y \
    ca-certificates \
    curl \
    gcc \
    libcurl4-gnutls-dev \
    zlib1g-dev \
    wget \
    tar \
    bzip2 \
    make \
    libgsl-dev \
    libbz2-dev \
    liblzma-dev \
    libperl-dev \
    libgsl-dev \
    xz-utils \
    libcurl4-gnutls-dev \
    libssl-dev \
    libgsl0-dev

# Install HTSlib 
RUN wget https://github.com/samtools/htslib/releases/download/${HTSLIB_VER}/htslib-${HTSLIB_VER}.tar.bz2 && \
    tar jxf htslib-${HTSLIB_VER}.tar.bz2 && \
    cd htslib-${HTSLIB_VER} && ./configure && make && make install && \
    cd / && \
    rm htslib-${HTSLIB_VER}.tar.bz2 && \
    rm -rf htslib-${HTSLIB_VER}

# Install BCFTools
RUN wget https://github.com/samtools/bcftools/releases/download/${BCFTOOLS_VER}/bcftools-${BCFTOOLS_VER}.tar.bz2 -q --show-progress &&\
    tar jxf bcftools-${BCFTOOLS_VER}.tar.bz2 &&\
    cd bcftools-${BCFTOOLS_VER} && ./configure --enable-libgsl && make && make install && cd / &&\
    rm bcftools-${BCFTOOLS_VER}.tar.bz2 &&\
    rm -rf bcftools-${BCFTOOLS_VER}

# Stage 2: Final Stage
FROM python:3.8.13-slim-bullseye
ARG TRANSPARSER_VER=1.0.1
ENV PATH=/transParser-1.0.1:$PATH

# Set labels for metadata
LABEL org.opencontainers.image.title="transParser"
LABEL org.opencontainers.image.version="1.0.1"
LABEL org.opencontainers.image.description="transParser is a tool that extracts the translocations (TRA) of a Manta's VCF and count the Number of Derivative Calls in some given named regions"
LABEL org.opencontainers.image.url="https://github.com/tgen/transParser"
LABEL org.opencontainers.image.licenses="https://github.com/tgen/transParser/blob/master/LICENSE"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"

# Copy TransParser Application from the Build Stage to the final image
COPY --from=build /usr/local/ /usr/local

# Install Required Packages and Clean Cache
RUN apt-get update -y && apt-get upgrade -y && apt-get install --no-install-recommends -y \
    bc \
    libcurl3-gnutls \
    libgsl25 &&\
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean

# Copy of TransParser tarball
COPY transParser-1.0.1.tar.gz /

# Install transParser
RUN tar zxf transParser-${TRANSPARSER_VER}.tar.gz &&\
    rm transParser-${TRANSPARSER_VER}.tar.gz &&\  
    cd transParser-${TRANSPARSER_VER} &&\
    chmod a+x transParser.*

# Create Working Directory
WORKDIR /data