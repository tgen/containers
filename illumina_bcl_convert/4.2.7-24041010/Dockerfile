FROM docker.io/library/rockylinux:8.9.20231119-minimal as build

ARG BCL_CONVERT_VER=4.2.7

# Install Dependencies
RUN microdnf upgrade -y && microdnf install -y \
    wget

# Install
RUN wget https://s3.amazonaws.com/webdata.illumina.com/downloads/software/bcl-convert/bcl-convert-${BCL_CONVERT_VER}-2.el8.x86_64.rpm

#____________________________________________________________________________________________
# Starting 2nd Stage
FROM docker.io/library/rockylinux:8.9.20231119-minimal

#=====================================================================================
LABEL org.opencontainers.image.title="illumina_bcl_convert"
LABEL org.opencontainers.image.version="4.2.7"
LABEL org.opencontainers.image.description="An application that converts the Binary Base Call (BCL) files produced by Illumina sequencing systems to FASTQ files"
LABEL org.opencontainers.image.url="https://support.illumina.com/sequencing/sequencing_software/bcl-convert.html"
LABEL org.opencontainers.image.licenses="https://www.illumina.com/company/legal.html"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES’ RIGHTS AND ANY WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"
#=====================================================================================

ARG BCL_CONVERT_VER=4.2.7

# Copy Application from 1st Build Stage
COPY --from=build /bcl-convert-${BCL_CONVERT_VER}-2.el8.x86_64.rpm /bcl-convert-${BCL_CONVERT_VER}-2.el8.x86_64.rpm

# Install Required Packages and Clean Cache
RUN microdnf upgrade -y && microdnf install -y \
    gdb &&\
    rpm -i ./bcl-convert-${BCL_CONVERT_VER}-2.el8.x86_64.rpm && rm ./bcl-convert-${BCL_CONVERT_VER}-2.el8.x86_64.rpm &&\
    microdnf clean all

# Create Working Directory
WORKDIR /data
