# Stage 1: Build Stage
FROM python:3.8.13-slim-bullseye
ENV PATH=$PATH:/tHReD-1.1.0

# Set labels for metadata
LABEL org.opencontainers.image.title="tHReD"
LABEL org.opencontainers.image.version="1.1.0"
LABEL org.opencontainers.image.description="TGen Homologous Recombination Deficiency (HRD) Tool to calculate HRD score ala TGen."
LABEL org.opencontainers.image.url="https://github.com/tgen/tHReD"
LABEL org.opencontainers.image.licenses="https://github.com/tgen/tHReD/blob/main/LICENSE"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"

COPY tHReD-1.1.0.tar.gz /

# Install Dependencies
RUN apt-get update && apt-get install --no-install-recommends -y \
    tar && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean

RUN python -m pip install natsort pandas matplotlib

# Extract THRED 
RUN tar zxf tHReD-1.1.0.tar.gz &&\
    rm -rf tHReD-1.1.0.tar.gz &&\
    chmod a+x tHReD-1.1.0/tHReD.py

# Create Working Directory
WORKDIR /data 