# Stage 1: Build Stage
FROM debian:bullseye-20230208-slim as build
ARG BWA_MEM2_VER=2.2.1
ARG SAMTOOLS_VER=1.17

# Install Dependencies
RUN apt-get update -y && apt-get upgrade -y && apt-get install -y \
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

# Install Samtools in static mode
RUN wget -qO- https://github.com/samtools/samtools/releases/download/${SAMTOOLS_VER}/samtools-${SAMTOOLS_VER}.tar.bz2 | tar -xjf - && \
    cd samtools-${SAMTOOLS_VER}/ && \
    ./configure CC="gcc -static" --without-curses && \
    make && make install

# Install Bwa-Mem2
RUN wget https://github.com/bwa-mem2/bwa-mem2/releases/download/v${BWA_MEM2_VER}/bwa-mem2-${BWA_MEM2_VER}_x64-linux.tar.bz2 && \
    tar xjf bwa-mem2-${BWA_MEM2_VER}_x64-linux.tar.bz2 && \
    rm bwa-mem2-${BWA_MEM2_VER}_x64-linux.tar.bz2 && \
    mv bwa-mem2-${BWA_MEM2_VER}_x64-linux bwa-mem2 && \
    mv /bwa-mem2/bwa* /usr/local/bin/

# Final stage
FROM trinityrnaseq/trinityrnaseq:2.8.6

# Set labels for metadata
LABEL org.opencontainers.image.title="trinity_bwa_samtools"
LABEL org.opencontainers.image.version="2.8.6_2.2.1_1.17"
LABEL org.opencontainers.image.description="Trinity RNA-Seq de novo transcriptome assembly."
LABEL org.opencontainers.image.citation="Grabherr MG, Haas BJ, Yassour M, Levin JZ, Thompson DA, Amit I, Adiconis X, Fan L, Raychowdhury R, Zeng Q, Chen Z, Mauceli E, Hacohen N, Gnirke A, Rhind N, di Palma F, Birren BW, Nusbaum C, Lindblad-Toh K, Friedman N, Regev A. Full-length transcriptome assembly from RNA-seq data without a reference genome. Nat Biotechnol. 2011 May 15;29(7):644-52. doi: 10.1038/nbt.1883. PubMed PMID: 21572440."
LABEL org.opencontainers.image.url="https://github.com/trinityrnaseq/trinityrnaseq"
LABEL org.opencontainers.image.licenses="https://github.com/trinityrnaseq/trinityrnaseq/blob/v2.8.6/LICENSE"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"

COPY --from=build /usr/local/ /usr/local
