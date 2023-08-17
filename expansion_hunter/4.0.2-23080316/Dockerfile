# Stage 1: Build Stage
FROM debian:bullseye-20230208-slim as build
ARG EXPANSION_HUNTER_VER=4.0.2

# Install Dependencies
RUN apt-get update -y && apt-get upgrade -y && apt-get install -y \
    wget \
    tar

# Install Expansion Hunter
RUN wget https://github.com/Illumina/ExpansionHunter/releases/download/v${EXPANSION_HUNTER_VER}/ExpansionHunter-v${EXPANSION_HUNTER_VER}-linux_x86_64.tar.gz &&\
    tar zxf ExpansionHunter-v${EXPANSION_HUNTER_VER}-linux_x86_64.tar.gz &&\
    rm -rf ExpansionHunter-v${EXPANSION_HUNTER_VER}-linux_x86_64.tar.gz &&\
    mv ExpansionHunter-v${EXPANSION_HUNTER_VER}-linux_x86_64/bin/ExpansionHunter /usr/local/bin/ &&\
    mv ExpansionHunter-v4.0.2-linux_x86_64/variant_catalog/* /usr/local/lib/

# Stage 2: Final Stage
FROM debian:bullseye-20230208-slim

# Set labels for metadata
LABEL org.opencontainers.image.title="ExpansionHunter"
LABEL org.opencontainers.image.version="4.0.2"
LABEL org.opencontainers.image.description="Expansion Hunter aims to estimate sizes of such repeats by performing a targeted search through a BAM/CRAM file for reads that span, flank, and are fully contained in each repeat."
LABEL org.opencontainers.image.citation="Egor Dolzhenko, Viraj Deshpande, Felix Schlesinger, Peter Krusche, Roman Petrovski, and others, ExpansionHunter: A sequence-graph based tool to analyze variation in short tandem repeat regions, Bioinformatics 2019"
LABEL org.opencontainers.image.url="https://github.com/Illumina/ExpansionHunter"
LABEL org.opencontainers.image.licenses="https://github.com/Illumina/ExpansionHunter/blob/v4.0.2/LICENSE.txt"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"

# Copy Expansion Hunter Application from the Build Stage to the final image
COPY --from=build /usr/local/ /usr/local

# Install Expansion Hunter Required Packages and Clean Cache
RUN apt-get update -y && apt-get upgrade -y && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean

# Create Working Directory
WORKDIR /data