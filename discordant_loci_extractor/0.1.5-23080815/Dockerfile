# Stage 1: Build Stage
FROM python:3.7.16-slim-bullseye as build
ARG DLE_VER=0.1.5
ENV VIRTUAL_ENV=/usr/local/python3
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

COPY Discordant_Loci_Extractor-0.1.5.tar.gz /

RUN apt update && apt upgrade -y && apt install --no-install-recommends -y \
    gcc \
    make \
    libc6-dev \
    zlib1g-dev \
    libbz2-dev \
    liblzma-dev \
    libcurl4-gnutls-dev \
    libssl-dev &&\

    python -m venv $VIRTUAL_ENV &&\
    pip install --no-cache-dir pysam==0.15.3 biopython==1.78 scipy==1.3.1 &&\
    tar zxf Discordant_Loci_Extractor-0.1.5.tar.gz &&\
    chmod +x Discordant_Loci_Extractor-0.1.5/dle.py &&\
    mv /Discordant_Loci_Extractor-0.1.5 /Discordant_Loci_Extractor

# Stage 2: Final Stage
FROM python:3.7.16-slim-bullseye

# Set labels for metadata
LABEL org.opencontainers.image.title="discordant_loci_extractor"
LABEL org.opencontainers.image.version="0.1.5"
LABEL org.opencontainers.image.description="Extract discordant read from a BAM/CRAM file and from specified small genomic regions, apply quick clustering, and write back the reads into fastq files"
LABEL org.opencontainers.image.url="https://github.com/tgen/Discordant_Loci_Extractor"
LABEL org.opencontainers.image.licenses="https://github.com/tgen/Discordant_Loci_Extractor/blob/main/LICENSE"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"

ENV VIRTUAL_ENV=/usr/local/python3
ENV PATH="$VIRTUAL_ENV/bin:/Discordant_Loci_Extractor:$PATH"

# Copy Discordant_Loci_Extractor Application from the Build Stage to the final image
COPY --from=build /usr/local/ /usr/local
COPY --from=build /Discordant_Loci_Extractor /Discordant_Loci_Extractor

RUN apt-get update && \
    apt-get install --no-install-recommends -y \
    libc6 \
    zlib1g \
    libbz2-1.0 \
    liblzma5 \
    libcurl3-gnutls \
    libssl1.1 &&\

# Clean apt cache.
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean

# Create Working Directory
WORKDIR /data