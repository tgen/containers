FROM python:3.10.19-trixie

# Install Dependencies
RUN apt-get update -y && apt-get upgrade -y && apt-get install -y \
    ca-certificates &&\
    pip install --upgrade pip &&\
    pip install pod5==0.3.35

# Create Working Directory
WORKDIR /data

LABEL org.opencontainers.image.title="pod5"
LABEL org.opencontainers.image.version="0.3.35"
LABEL org.opencontainers.image.description="POD5 is a file format for storing nanopore dna data in an easily accessible way. The format is able to be written in a streaming manner which allows a sequencing instrument to directly write the format."
LABEL org.opencontainers.image.url="https://github.com/nanoporetech/pod5-file-format"
LABEL org.opencontainers.image.licenses="https://github.com/nanoporetech/pod5-file-format/blob/master/LICENSE.md"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided  “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"
