FROM docker.io/library/centos:7.9.2009

ARG BCL_CONVERT_VER=3.9.3

# bcl-convert is behind a loging for download and must be downloaded first
# and be placed in the build directory.
COPY bcl-convert-3.9.3-2.el7.x86_64.rpm /

# Install Required Packages and Clean Cache
RUN yum upgrade -y && yum install -y \
    gdb &&\
    rpm -i ./bcl-convert-${BCL_CONVERT_VER}-2.el7.x86_64.rpm && rm ./bcl-convert-${BCL_CONVERT_VER}-2.el7.x86_64.rpm &&\
    yum clean all

# Create Working Directory
WORKDIR /data

#=====================================================================================
LABEL org.opencontainers.image.title="illumina_bcl_convert"
LABEL org.opencontainers.image.version="3.9.3"
LABEL org.opencontainers.image.description="An application that converts the Binary Base Call (BCL) files produced by Illumina sequencing systems to FASTQ files"
LABEL org.opencontainers.image.url="https://support.illumina.com/sequencing/sequencing_software/bcl-convert.html"
LABEL org.opencontainers.image.licenses="https://www.illumina.com/company/legal.html"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES’ RIGHTS AND ANY WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"
#=====================================================================================
