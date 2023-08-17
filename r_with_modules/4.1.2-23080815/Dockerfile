# Stage 1: Build Stage
FROM rocker/r-ver:4.1.2 as build

# R build dependencies based on https://github.com/rocker-org/rocker-versioned2/blob/master/scripts/install_tidyverse.sh#L18-L35
RUN apt-get update && apt-get install --no-install-recommends -y \
    zlib1g-dev \
    libxml2-dev \
    liblzma-dev \
    libbz2-dev \
    libicu-dev \
    libcairo2-dev \
    libgit2-dev \
    libmysqlclient-dev \
    libpq-dev \
    libsasl2-dev \
    libsqlite3-dev \
    libssh2-1-dev \
    libxtst-dev \
    libxt-dev \
    libcurl4-openssl-dev \
    libharfbuzz-dev \
    libfribidi-dev \
    libfreetype6-dev \
    libpng-dev \
    libtiff5-dev \
    libjpeg-dev \
    unixodbc-dev

RUN Rscript -e 'install.packages("tidyverse"); install.packages("optparse"); install.packages("data.table")'
RUN sed -i "s/options(show.error.messages = TRUE)/options(bitmapType='cairo')/g" /usr/local/lib/R/library/base/R/Rprofile

# Stage 2: Final Stage
FROM rocker/r-ver:4.1.2

# Set labels for metadata
LABEL org.opencontainers.image.title="r with modules"
LABEL org.opencontainers.image.version="4.1.2"
LABEL org.opencontainers.image.description="R is a language and environment for statistical computing and graphics."
LABEL org.opencontainers.image.url="https://www.r-project.org/"
LABEL org.opencontainers.image.licenses="https://www.r-project.org/COPYING"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"

# Copy R and new libraries from the Build Stage to the final image
COPY --from=build /usr/local/ /usr/local

# Install required packages and clean cache
RUN apt-get update && apt-get install --no-install-recommends -y \
    zlib1g \
    libxml2 \
    liblzma5 \
    libbz2-1.0 \
    libc6 \
    libcairo2 \
    libgit2-28 \
    libmysqlclient21 \
    libpq5 \
    libsasl2-2 \
    libsqlite3-0 \
    libssh2-1 \
    libxtst6 \
    libxt6 \
    libcurl4 \
    libharfbuzz0b \
    libfribidi0 \
    libfreetype6 \
    libpng16-16 \
    libtiff5 \
    libjpeg8 \
    unixodbc-dev && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoclean

# Create Working Directory
WORKDIR /data