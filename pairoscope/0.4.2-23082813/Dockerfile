# Stage 1: Build Stage
FROM debian:bullseye-20230208-slim as build
ARG PAIROSCOPE_VER=0.4.2

# Install necessary dependencies
RUN apt-get update -y && apt-get upgrade -y && apt-get install -y \
    build-essential \
    cmake \
    wget \
    tar \
    libfreetype6-dev \
    libcairo2-dev \
    libncurses-dev

# Install pairoscope
RUN wget https://github.com/genome/pairoscope/archive/refs/tags/v${PAIROSCOPE_VER}.tar.gz -q --show-progress &&\
    tar zxf v${PAIROSCOPE_VER}.tar.gz &&\
    rm v${PAIROSCOPE_VER}.tar.gz &&\
    mkdir pairoscope-${PAIROSCOPE_VER}/build &&\
    cd pairoscope-${PAIROSCOPE_VER}/build &&\
    cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_CXX_FLAGS=-pthread .. &&\
    make  &&\
    make install  &&\
    cd / &&\
    rm -rf pairoscope-${PAIROSCOPE_VER}

# Stage 2: Final Stage
FROM debian:bullseye-20230208-slim

# Set labels for metadata
LABEL org.opencontainers.image.title="pairoscope"
LABEL org.opencontainers.image.version="0.4.2"
LABEL org.opencontainers.image.description="Pairoscope generates simple static plots of read pairing information. It is useful for viewing putative SV calls from callers that utilize insert size metrics and read pair orientation."
LABEL org.opencontainers.image.url="https://github.com/genome/pairoscope"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"

# Copy Pairoscope Application from the Build Stage to the final image
COPY --from=build /usr/bin/ /usr/bin

# Install Required Packages and Clean Cache
RUN apt-get update -y && apt-get upgrade -y && apt-get install  -y \
    libcairo2 &&\
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean

# Create Working Directory
WORKDIR /data