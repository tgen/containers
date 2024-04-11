FROM rocker/r-ver:4.3.3

COPY module_install.sh /module_install.sh
COPY R_modules.csv /R_modules.csv

# Install Dependencies
RUN apt-get update -y && apt-get upgrade -y && apt-get install -y \
    ca-certificates \
    wget \
    curl \
    libcairo2-dev \
    cmake \
    libcurl4-gnutls-dev \
    libssl-ocaml-dev \
    libharfbuzz-dev \
    libfribidi-dev \
    libfreetype6-dev \
    libpng-dev \
    libtiff5-dev \
    libjpeg-dev \
    libxml2-dev \
    libbz2-dev &&\

    bash -x module_install.sh &&\
    rm /module_install.sh && rm /R_modules.csv &&\

    Rscript -e 'devtools::install_github("hdng/clonevol")' &&\
    Rscript -e 'devtools::install_github("hdng/trees")' &&\
    Rscript -e 'devtools::install_github("pachterlab/sleuth")'

#=====================================================================================
    LABEL org.opencontainers.image.title="r"
    LABEL org.opencontainers.image.version="4.3.3"
    LABEL org.opencontainers.image.description="R is a system for statistical computation and graphics. It consists of a language plus a run-time environment with graphics, a debugger, access to certain system functions, and the ability to run programs stored in script files.'https://www.r-project.org/COPYING'"
    LABEL org.opencontainers.image.url="https://www.r-project.org/"
    LABEL org.opencontainers.image.licenses="https://www.gnu.org/licenses/old-licenses/gpl-2.0.html"
    LABEL org.opencontainers.image.authors="TGen Containers"
    LABEL org.opencontainers.image.authors.email="containers@tgen.org"
    LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES’ RIGHTS AND ANY WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
    LABEL org.opencontainers.image.source="https://github.com/tgen/containers"
#=====================================================================================