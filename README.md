Containers
--------
Inspired by [BioContainers](https://github.com/BioContainers/containers). This [containers](https://github.com/tgen/containers) repository hosts bioinformatics
containers validated by The Translational Genomics Research Institute (TGen).

__Disclaimer__: 
> These containers are for academic and non-commercial research and educational purposes only. These containers are provided “AS IS” without any warranty of any
kind, express or implied. TGen expressly disclaims all warranties of MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, and NON-INFRINGEMENT OF THIRD PARTIES’ RIGHTS AND ANY 
WARRANTIES OR GUARANTEES OF ANY PARTICULAR RESULTS OR OUTCOMES. You assume all risk and liability for any access or use. IN NO EVENT SHALL TGEN OR ANY PROVIDERS OR CONTRIBUTORS 
BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS 
OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
> 
> All rights are reserved. Each container includes a copy of and/or a link to the licenses and copyright or other notices for the software tools in the container, and, by accessing
or using these containers, you agree to read and abide by them. If a link doesn’t work, contact TGen at containers@tgen.org.

## 1. Overview

### 1.1 Objectives

* Provide a series of containers ready to be used by the bioinformatics community that have been thoroughly tested and actively used within TGen's bioinformatics pipelines.

* Provide a more informatically relevant set of test cases per container
  * Example: Validating that `bcftools view test.vcf.gz chr21` gives the expected result.


## 2. Containers
| Tool | License | Version(s) Available |
| :---: | :---: | :---: |
| [samtools](https://github.com/samtools/samtools) | [MIT/Expat](https://github.com/samtools/samtools/blob/1.17/LICENSE) | [1.17](https://github.com/tgen/containers/pkgs/container/jetstream_containers%2Fdev-samtools/110309233?tag=1.17-23071709)<sup>[Dockerfile](samtools/1.17-23071709/Dockerfile)</sup> |