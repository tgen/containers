# Stage 1: Build Stage
FROM python:3.8.16-slim
ENV PATH=$PATH:/sigprofiler

# Set labels for metadata
LABEL org.opencontainers.image.title="sigprofiler"
LABEL org.opencontainers.image.version="0.0.24"
LABEL org.opencontainers.image.description="SigProfilerAssignment enables assignment of previously known mutational signatures to individual samples and individual somatic mutations. The tool refits different types of reference mutational signatures, including COSMIC signatures, as well as custom signature databases."
LABEL org.opencontainers.image.url="https://github.com/AlexandrovLab/SigProfilerAssignment"
LABEL org.opencontainers.image.licenses="https://github.com/AlexandrovLab/SigProfilerAssignment/blob/main/LICENSE.txt"
LABEL org.opencontainers.image.authors="TGen Containers"
LABEL org.opencontainers.image.authors.email="containers@tgen.org"
LABEL org.opencontainers.image.disclaimer="This container is for academic and non-commercial research and educational purposes only. This container is provided “AS IS” without any warranty of any kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES' RIGHTS AND ANY  WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE."
LABEL org.opencontainers.image.source="https://github.com/tgen/containers"

# wget is needed to pull signatures, genInstall.py will use rsync in specific environments
RUN sed -i 's/main/main contrib/g' /etc/apt/sources.list && \
    apt update && \
    apt install -y wget rsync ttf-mscorefonts-installer

# Install SigProfilerAssignment and dependencies with locked versions
COPY genInstall.py .
RUN pip install --upgrade pip && \
    pip install about-time==4.2.1 \
    alive-progress==3.0.1 \
    contourpy==1.0.7 \
    cycler==0.11.0 \
    fonttools==4.38.0 \
    grapheme==0.6.0 \
    joblib==1.2.0 \
    kiwisolver==1.4.4 \
    matplotlib==3.6.3 \
    numpy==1.24.1 \
    packaging==23.0 \
    pandas==1.5.3 \
    patsy==0.5.3 \
    pdf2image==1.16.2 \
    Pillow==9.4.0 \
    psutil==5.9.4 \
    PyMuPDF==1.21.1 \
    pyparsing==3.0.9 \
    PyPDF2==3.0.1 \
    python-dateutil==2.8.2 \
    pytz==2022.7.1 \
    reportlab==3.6.12 \
    scikit-learn==1.2.1 \
    scipy==1.10.0 \
    SigProfilerAssignment==0.0.24 \
    SigProfilerMatrixGenerator==1.2.13 \
    sigProfilerPlotting==1.3.10 \
    six==1.16.0 \
    statsmodels==0.13.5 \
    threadpoolctl==3.1.0 \
    typing_extensions==4.4.0 && \
    python genInstall.py && rm genInstall.py

# Copy in sigprofiler_assignment script
WORKDIR /sigprofiler
COPY sigprofiler_assignment.py .
RUN chmod +x sigprofiler_assignment.py

# Pull GRCh38 signatures for sigprofiler
WORKDIR /sigprofiler_resources
RUN wget https://cancer.sanger.ac.uk/signatures/documents/2047/COSMIC_v3.3.1_SBS_GRCh38.txt && \
    wget https://cancer.sanger.ac.uk/signatures/documents/1903/COSMIC_v3.3_DBS_GRCh38.txt

WORKDIR /
