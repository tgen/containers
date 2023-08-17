# Stage 1: Build Stage
FROM debian:bullseye-20230208-slim as build
ARG STRELKA_VER=2.9.10

# Install Dependencies
RUN apt-get update -y && apt-get upgrade -y && apt-get install --no-install-recommends -y \
    wget \
    make \
    cmake \
    bzip2 \
    tar \
    gcc \
    zlib1g-dev \
    libboost-all-dev \
    g++ \
    ca-certificates \
    python && \
    apt-get autoclean

# Install strelka
RUN wget https://github.com/Illumina/strelka/releases/download/v${STRELKA_VER}/strelka-${STRELKA_VER}.release_src.tar.bz2 -q --show-progress && \
    tar -xjf strelka-${STRELKA_VER}.release_src.tar.bz2 && \
    mkdir build && \
    cd build && \
    ../strelka-${STRELKA_VER}.release_src/configure --jobs=4 --prefix=/usr/local && \
    make -j4 install && \
    cd / &&\
    rm -rf build strelka-${STRELKA_VER}.release_src strelka-${STRELKA_VER}.release_src.tar.bz2

# Stage 2: Final Stage
FROM debian:bullseye-20230208-slim

# Set labels for metadata
LABEL org.opencontainers.image.title="strelka"
LABEL org.opencontainers.image.version="2.9.10"
LABEL org.opencontainers.image.description="Strelka2 is a fast and accurate small variant caller optimized for analysis of germline variation in small cohorts and somatic variation in tumor/normal sample pairs."
LABEL org.opencontainers.image.citation="Kim, S., Scheffler, K. et al. (2018) Strelka2: fast and accurate calling of germline and somatic variants. Nature Methods, 15, 591-594. doi:10.1038/s41592-018-0051-x"
LABEL org.opencontainers.image.url="https://github.com/Illumina/strelka"
LABEL org.opencontainers.image.licenses="https://github.com/Illumina/strelka/blob/v2.9.10/LICENSE.txt"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"

# Copy strelka Application from the Build Stage to the final image
COPY --from=build /usr/local/ /usr/local

# Install Required Packages and Clean Cache
RUN apt-get update -y && apt-get upgrade -y && apt-get install --no-install-recommends -y \
    python && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean

# Create Working Directory 
WORKDIR /data