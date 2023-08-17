# Stage 1: Build Stage
FROM debian:bullseye-20230208-slim as build
ARG LANCET_VER=1.1.x

# Install requirements for lancet
RUN apt-mark hold tzdata && apt-get update && apt-get install --no-install-recommends -y \
    wget \
    ca-certificates \
    unzip \
    cmake \
    g++ \
    make \
    liblzma-dev \
    libcurl4-gnutls-dev \
    zlib1g-dev \
    libbz2-dev \
    libssl-dev

# Download and install lancet
RUN wget https://github.com/nygenome/lancet/archive/v${LANCET_VER}.zip -q --show-progress && \
    unzip v${LANCET_VER}.zip && \
    rm v${LANCET_VER}.zip && \
    cd lancet-${LANCET_VER} && \
    make && \
    mv lancet /usr/local/bin && \
    cd / && \
    rm -rf lancet-${LANCET_VER}

# Stage 2: Final Stage
FROM debian:bullseye-20230208-slim

# Set labels for metadata
LABEL org.opencontainers.image.title="lancet"
LABEL org.opencontainers.image.version="1.1.x"
LABEL org.opencontainers.image.description="Lancet is a somatic variant caller (SNVs and indels) for short read data. Lancet uses a localized micro-assembly strategy to detect somatic mutation with high sensitivity and accuracy on a tumor/normal pair."
LABEL org.opencontainers.image.citation="Narzisi G, Corvelo A, Arora K, Bergmann E, Shah M, Musunuri R, Emde AK, Robine N, Vacic V, Zody MC. Genome-wide somatic variant calling using localized colored de Bruijn graphs. Communications Biology, Nature Research publishing, volume 1, Article number: 20, 2018"
LABEL org.opencontainers.image.url="https://github.com/nygenome/lancet"
LABEL org.opencontainers.image.licenses="https://github.com/nygenome/lancet/blob/v1.1.x/LICENSE.txt"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"

# Copy Lancet Application from the Build Stage to the final image
COPY --from=build /usr/local/ /usr/local

# Install Bcftools Required Packages and Clean Cache
RUN apt-mark hold tzdata && apt-get update -y && apt-get install --no-install-recommends -y \
    libcurl3-gnutls && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean

# Create Working Directory
WORKDIR /data