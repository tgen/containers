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
| [bcftools](https://github.com/samtools/bcftools) | [LICENSE](https://github.com/samtools/bcftools/blob/1.17/LICENSE) | [1.17](https://ghcr.io/tgen/containers/bcftools:1.17)<sup>[Dockerfile](bcftools/1.17/Dockerfile)</sup> |
| [bedtools](https://github.com/arq5x/bedtools2) | [LICENSE](https://github.com/arq5x/bedtools2/blob/v2.29.0/LICENSE) | [2.29.0](https://ghcr.io/tgen/containers/bedtools:2.29.0)<sup>[Dockerfile](bedtools/2.29.0/Dockerfile)</sup> |
| [bwa-mem2](https://github.com/bwa-mem2/bwa-mem2) | [LICENSE](https://github.com/bwa-mem2/bwa-mem2/blob/v2.2.1/LICENSE) | [2.2.1](https://ghcr.io/tgen/containers/bwa-mem2:2.2.1)<sup>[Dockerfile](bwa-mem2/2.2.1/Dockerfile)</sup> |
| [discordant_loci_extractor](https://github.com/tgen/Discordant_Loci_Extractor) | [LICENSE](https://github.com/tgen/Discordant_Loci_Extractor/blob/main/LICENSE) | [0.1.5](https://ghcr.io/tgen/containers/discordant_loci_extractor:0.1.5)<sup>[Dockerfile](discordant_loci_extractor/0.1.5/Dockerfile)</sup> |
| [ExpansionHunter](https://github.com/Illumina/ExpansionHunter) | [LICENSE](https://github.com/Illumina/ExpansionHunter/blob/v4.0.2/LICENSE.txt) | [4.0.2](https://ghcr.io/tgen/containers/ExpansionHunter:4.0.2)<sup>[Dockerfile](ExpansionHunter/4.0.2/Dockerfile)</sup> |
| [Fgbio](https://github.com/fulcrumgenomics/fgbio) | [LICENSE](https://github.com/fulcrumgenomics/fgbio/blob/2.0.2/LICENSE) | [2.0.2](https://ghcr.io/tgen/containers/Fgbio:2.0.2)<sup>[Dockerfile](Fgbio/2.0.2/Dockerfile)</sup> |
| [htslib](https://github.com/samtools/htslib) | [LICENSE](https://github.com/samtools/htslib/blob/1.17/LICENSE) | [1.17](https://ghcr.io/tgen/containers/htslib:1.17)<sup>[Dockerfile](htslib/1.17/Dockerfile)</sup> |
| [lancet](https://github.com/nygenome/lancet) | [LICENSE](https://github.com/nygenome/lancet/blob/v1.1.x/LICENSE.txt) | [1.1.x](https://ghcr.io/tgen/containers/lancet:1.1.x)<sup>[Dockerfile](lancet/1.1.x/Dockerfile)</sup> |
| [manta](https://github.com/Illumina/manta) | [LICENSE](https://github.com/Illumina/manta/blob/v1.6.0/LICENSE.txt) | [1.6.0](https://ghcr.io/tgen/containers/manta:1.6.0)<sup>[Dockerfile](manta/1.6.0/Dockerfile)</sup> |
| [MSISensor](https://github.com/xjtu-omics/msisensor-pro) | [LICENSE](https://github.com/xjtu-omics/msisensor-pro/blob/master/LICENSE) | [1.1.a](https://ghcr.io/tgen/containers/MSISensor:1.1.a)<sup>[Dockerfile](MSISensor/1.1.a/Dockerfile)</sup> |
| [tgen_mutation_burden](https://github.com/tgen/tgen_mutation_burden) | [LICENSE](https://github.com/tgen/tgen_mutation_burden/blob/master/LICENSE) | [1.2.4](https://ghcr.io/tgen/containers/tgen_mutation_burden:1.2.4)<sup>[Dockerfile](tgen_mutation_burden/1.2.4/Dockerfile)</sup> |
| [octopus](https://github.com/luntergroup/octopus) | [LICENSE](https://github.com/luntergroup/octopus/blob/v0.7.4/LICENSE) | [0.7.4](https://ghcr.io/tgen/containers/octopus:0.7.4)<sup>[Dockerfile](octopus/0.7.4/Dockerfile)</sup> |
| [pairoscope](https://github.com/genome/pairoscope) | [LICENSE]() | [0.4.2](https://ghcr.io/tgen/containers/pairoscope:0.4.2)<sup>[Dockerfile](pairoscope/0.4.2/Dockerfile)</sup> |
| [r with modules](https://www.r-project.org/) | [LICENSE](https://www.r-project.org/COPYING) | [4.1.2](https://ghcr.io/tgen/containers/r with modules:4.1.2)<sup>[Dockerfile](r with modules/4.1.2/Dockerfile)</sup> |
| [samtools]() | [LICENSE]() | [](https://ghcr.io/tgen/containers/samtools:)<sup>[Dockerfile](samtools//Dockerfile)</sup> |
| [samtools](https://github.com/samtools/samtools) | [LICENSE](https://github.com/samtools/samtools/blob/1.17/LICENSE) | [1.17](https://ghcr.io/tgen/containers/samtools:1.17)<sup>[Dockerfile](samtools/1.17/Dockerfile)</sup> |
| [sigprofiler](https://github.com/AlexandrovLab/SigProfilerAssignment) | [LICENSE](https://github.com/AlexandrovLab/SigProfilerAssignment/blob/main/LICENSE.txt) | [0.0.24](https://ghcr.io/tgen/containers/sigprofiler:0.0.24)<sup>[Dockerfile](sigprofiler/0.0.24/Dockerfile)</sup> |
| [snpSniffer](https://github.com/tgen/snpSniffer) | [LICENSE](https://github.com/tgen/snpSniffer/blob/v7.0.0/LICENSE) | [7.0.0](https://ghcr.io/tgen/containers/snpSniffer:7.0.0)<sup>[Dockerfile](snpSniffer/7.0.0/Dockerfile)</sup> |
| [strelka](https://github.com/Illumina/strelka) | [LICENSE](https://github.com/Illumina/strelka/blob/v2.9.10/LICENSE.txt) | [2.9.10](https://ghcr.io/tgen/containers/strelka:2.9.10)<sup>[Dockerfile](strelka/2.9.10/Dockerfile)</sup> |
| [tHReD](https://github.com/tgen/tHReD) | [LICENSE](https://github.com/tgen/tHReD/blob/main/LICENSE) | [1.1.0](https://ghcr.io/tgen/containers/tHReD:1.1.0)<sup>[Dockerfile](tHReD/1.1.0/Dockerfile)</sup> |
| [transParser](https://github.com/tgen/transParser) | [LICENSE](https://github.com/tgen/transParser/blob/master/LICENSE) | [1.0.1](https://ghcr.io/tgen/containers/transParser:1.0.1)<sup>[Dockerfile](transParser/1.0.1/Dockerfile)</sup> |
| [vcfMerger2](https://github.com/tgen/vcfMerger2) | [LICENSE](https://github.com/tgen/vcfMerger2/blob/v0.9.4/LICENSE.md) | [0.9.4](https://ghcr.io/tgen/containers/vcfMerger2:0.9.4)<sup>[Dockerfile](vcfMerger2/0.9.4/Dockerfile)</sup> |
