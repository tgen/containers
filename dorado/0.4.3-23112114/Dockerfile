FROM debian:bullseye-20230208-slim as build
ARG DORADO_VER=0.4.3

# Install Dependencies
RUN apt-get update -y && apt-get install -y \
	curl \
	git \
	build-essential \
    ca-certificates \
    libhdf5-dev \
    libssl-dev \
    libzstd-dev \
    wget

# Install Dorado
RUN wget -qO- https://cdn.oxfordnanoportal.com/software/analysis/dorado-${DORADO_VER}-linux-x64.tar.gz | \
    tar -xzf -
RUN cp -R dorado-${DORADO_VER}*/bin/* /usr/local/bin && \
    cp -R dorado-${DORADO_VER}*/lib/* /usr/local/lib

# Starting 2nd Stage
FROM debian:bullseye-20230208-slim

# Set labels for metadata
LABEL org.opencontainers.image.title="dorado"
LABEL org.opencontainers.image.version="0.4.3"
LABEL org.opencontainers.image.description="Dorado is a high-performance, easy-to-use, open source basecaller for Oxford Nanopore reads."
LABEL org.opencontainers.image.url="https://github.com/nanoporetech/dorado"
LABEL org.opencontainers.image.licenses="https://github.com/nanoporetech/dorado/blob/v0.4.3/LICENCE.txt"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided  “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"

# Copy Dorado Application from 1st Build Stage
COPY --from=build /usr/local/ /usr/local

# Install Required Packages and Clean Cache
RUN apt-get update -y && apt-get install -y \
    ca-certificates \
    curl && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean

# Create Working Directory
WORKDIR /data
