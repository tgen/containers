FROM debian:bullseye-20230208-slim as build

ARG FastQC_VER=0.12.1

# Install Dependencies
RUN apt-get update -y && apt-get upgrade -y && apt-get install -y \
    ca-certificates \
    wget \
    unzip \
    openjdk-17-jdk \
    libfindbin-libs-perl

# Install
RUN wget https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v${FastQC_VER}.zip &&\
    unzip fastqc_v${FastQC_VER}.zip

#____________________________________________________________________________________________
# Starting 2nd Stage
FROM debian:bullseye-20230208-slim
#===================================================================================== 
LABEL org.opencontainers.image.title="FastQC"
LABEL org.opencontainers.image.version="0.12.1"
LABEL org.opencontainers.image.description="A quality control analysis tool for high throughput sequencing data"
LABEL org.opencontainers.image.url="https://github.com/s-andrews/FastQC/releases/tag/v0.12.1"
LABEL org.opencontainers.image.licenses="https://github.com/s-andrews/FastQC/blob/v0.12.1/LICENSE.txt"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES’ RIGHTS AND ANY WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers" 
#===========================================================
ENV PATH /FastQC:$PATH

# Copy Application from 1st Build Stage
COPY --from=build /FastQC/ /FastQC

# Install Required Packages and Clean Cache
RUN apt-get update -y && apt-get upgrade -y && apt-get install --no-install-recommends -y \
    openjdk-17-jdk \
    libfindbin-libs-perl \
    imagemagick &&\
    
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean

# Create Working Directory
WORKDIR /data
