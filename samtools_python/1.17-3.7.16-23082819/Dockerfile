# Samtools build stage
FROM debian:bullseye-20230208-slim as samtools_build
ARG SAMTOOLS_VER=1.17

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

# Python build stage
FROM python:3.7.16-slim-bullseye as python_build

ENV VIRTUAL_ENV=/usr/local/python3
RUN python -m venv $VIRTUAL_ENV
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

# Install build dependencies
RUN apt-get update &&  apt-get install --no-install-recommends -y \
      gcc \
      zlib1g-dev \
      libbz2-dev \
      liblzma-dev \
      make

# Upgrade pip and install required packages
RUN pip install --no-compile --no-cache-dir --upgrade pip && \
    pip install --no-compile --no-cache-dir --upgrade wheel && \
    pip install --no-compile --no-cache-dir \
        numpy==1.17.3 \
        pandas==0.25.3 \
        pysam==0.15.3

# Final stage
FROM python:3.7.16-slim-bullseye

# Set labels for metadata
LABEL org.opencontainers.image.title="samtools"
LABEL org.opencontainers.image.version="1.17"
LABEL org.opencontainers.image.description="Tools (written in C using htslib) for manipulating next-generation sequencing data"
LABEL org.opencontainers.image.citation="Twelve years of SAMtools and BCFtools Petr Danecek, James K Bonfield, Jennifer Liddle, John Marshall, Valeriu Ohan, Martin O Pollard, Andrew Whitwham, Thomas Keane, Shane A McCarthy, Robert M Davies, Heng Li GigaScience, Volume 10, Issue 2, February 2021, giab008, https://doi.org/10.1093/gigascience/giab008"
LABEL org.opencontainers.image.url="https://github.com/samtools/samtools"
LABEL org.opencontainers.image.licenses="https://github.com/samtools/samtools/blob/1.17/LICENSE"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"

ENV VIRTUAL_ENV=/usr/local/python3
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

COPY --from=python_build /usr/local/ /usr/local
COPY --from=samtools_build /usr/local/ /usr/local

# Install required libraries and clean cache
RUN apt-get update && \
    apt-get install --no-install-recommends -y \
      zlib1g \
      libbz2-1.0 \
      libncursesw6 \
      libcurl3-gnutls \
      liblzma5 && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean
