FROM python:3.8.13-slim-bullseye as build

ARG INTEROP_VER=1.3.1

# Install Dependencies
RUN apt-get update -y && apt-get upgrade -y && apt-get install -y \
    ca-certificates \
    wget &&\

# Install
    #pip install interop &&\
    wget https://github.com/Illumina/interop/releases/download/v${INTEROP_VER}/interop-${INTEROP_VER}-Linux-GNU.tar.gz &&\
    tar xf interop-${INTEROP_VER}-Linux-GNU.tar.gz

# Starting 2nd Stage
FROM python:3.8.13-slim-bullseye

# Copy Application from 1st Build Stage
COPY --from=build /interop-1.3.1-Linux-GNU/ /interop

ENV PATH=/interop/bin:$PATH
ARG DEBIAN_FRONTEND noninteractive

RUN apt-get update -y && apt-get upgrade -y &&\
    apt install -y gnuplot &&\

# Clean Cache
rm -rf /var/lib/apt/lists/* && \
apt-get autoclean

# Create Working Directory
WORKDIR /data

#=====================================================================================
LABEL org.opencontainers.image.title="illumina_interop" 
LABEL org.opencontainers.image.version="1.3.1" 
LABEL org.opencontainers.image.description="The Illumina InterOp libraries are a set of common routines used for reading InterOp metric files produced by Illumina sequencers"
LABEL org.opencontainers.image.url=" https://github.com/Illumina/interop/releases/tag/v1.3.1" 
LABEL org.opencontainers.image.licenses=" https://github.com/Illumina/interop/blob/v1.3.1/LICENSE" 
LABEL org.opencontainers.image.authors="TGen Containers" 
LABEL org.opencontainers.image.authors.email="containers@tgen.org" 
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES’ RIGHTS AND ANY WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers" 
LABEL other_software="Gnuplot v5.4.1"
#=====================================================================================
