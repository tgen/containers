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
| [bcftools](https://github.com/samtools/bcftools) | [LICENSE](https://github.com/samtools/bcftools/blob/1.17/LICENSE) | [1.17](https://ghcr.io/tgen/containers/bcftools)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/bcftools/1.17-23080313/Dockerfile)</sup> |
| [bedtools](https://github.com/arq5x/bedtools2) | [LICENSE](https://github.com/arq5x/bedtools2/blob/v2.29.0/LICENSE) | [2.29.0](https://ghcr.io/tgen/containers/bedtools)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/bedtools/2.29.0-23080313/Dockerfile)</sup> |
| [bwa_mem2_samtools](https://github.com/bwa-mem2/bwa-mem2) | [LICENSE](https://github.com/bwa-mem2/bwa-mem2/blob/v2.2.1/LICENSE) | [2.2.1](https://ghcr.io/tgen/containers/bwa_mem2_samtools)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/bwa_mem2_samtools/2.2.1-23080315/Dockerfile)</sup> |
| [discordant_loci_extractor](https://github.com/tgen/Discordant_Loci_Extractor) | [LICENSE](https://github.com/tgen/Discordant_Loci_Extractor/blob/main/LICENSE) | [0.1.5](https://ghcr.io/tgen/containers/discordant_loci_extractor)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/discordant_loci_extractor/0.1.5-23080815/Dockerfile)</sup> |
| [dorado](https://github.com/nanoporetech/dorado) | [LICENSE](https://github.com/nanoporetech/dorado/blob/v0.4.3/LICENCE.txt) | [0.4.3](https://ghcr.io/tgen/containers/dorado)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/dorado/0.4.3-23112114/Dockerfile)</sup> |
| [expansion_hunter](https://github.com/Illumina/ExpansionHunter) | [LICENSE](https://github.com/Illumina/ExpansionHunter/blob/v4.0.2/LICENSE.txt) | [4.0.2](https://ghcr.io/tgen/containers/expansion_hunter)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/expansion_hunter/4.0.2-23080316/Dockerfile)</sup> |
| [fgbio](https://github.com/fulcrumgenomics/fgbio) | [LICENSE](https://github.com/fulcrumgenomics/fgbio/blob/2.0.2/LICENSE) | [2.0.2](https://ghcr.io/tgen/containers/fgbio)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/fgbio/2.0.2-23082819/Dockerfile)</sup> |
| [htslib](https://github.com/samtools/htslib) | [LICENSE](https://github.com/samtools/htslib/blob/1.17/LICENSE) | [1.17](https://ghcr.io/tgen/containers/htslib)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/htslib/1.17-23080709/Dockerfile)</sup> |
| [lancet](https://github.com/nygenome/lancet) | [LICENSE](https://github.com/nygenome/lancet/blob/v1.1.x/LICENSE.txt) | [1.1.x](https://ghcr.io/tgen/containers/lancet)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/lancet/1.1.x-23080709/Dockerfile)</sup> |
| [manta](https://github.com/Illumina/manta) | [LICENSE](https://github.com/Illumina/manta/blob/v1.6.0/LICENSE.txt) | [1.6.0](https://ghcr.io/tgen/containers/manta)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/manta/1.6.0-23082819/Dockerfile)</sup> |
| [manta_tgen](https://github.com/tgen/manta) | [LICENSE](https://github.com/tgen/manta/blob/v1.6.0/LICENSE.txt) | [1.6.0](https://ghcr.io/tgen/containers/manta_tgen)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/manta_tgen/1.6.0-23082819/Dockerfile)</sup> |
| [msisensor](https://github.com/xjtu-omics/msisensor-pro) | [LICENSE](https://github.com/xjtu-omics/msisensor-pro/blob/master/LICENSE) | [1.1.a](https://ghcr.io/tgen/containers/msisensor)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/msisensor/1.1.a-23080815/Dockerfile)</sup> |
| [mutation-burden](https://github.com/tgen/tgen_mutation_burden) | [LICENSE](https://github.com/tgen/tgen_mutation_burden/blob/master/LICENSE) | [1.2.4](https://ghcr.io/tgen/containers/mutation-burden)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/mutation-burden/1.2.4-23080815/Dockerfile)</sup> |
| [octopus](https://github.com/luntergroup/octopus) | [LICENSE](https://github.com/luntergroup/octopus/blob/v0.7.4/LICENSE) | [0.7.4](https://ghcr.io/tgen/containers/octopus)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/octopus/0.7.4-23080809/Dockerfile)</sup> |
| [pairoscope](https://github.com/genome/pairoscope) | [LICENSE](https://github.com/genome/pairoscope) | [0.4.2](https://ghcr.io/tgen/containers/pairoscope)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/pairoscope/0.4.2-23082813/Dockerfile)</sup> |
| [pod5](https://github.com/nanoporetech/pod5-file-format) | [LICENSE](https://github.com/nanoporetech/pod5-file-format/blob/master/LICENSE.md) | [0.3.1](https://ghcr.io/tgen/containers/pod5)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/pod5/0.3.1-23112114/Dockerfile)</sup> |
| [r_with_modules](https://www.r-project.org/) | [LICENSE](https://www.r-project.org/COPYING) | [4.1.2](https://ghcr.io/tgen/containers/r_with_modules)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/r_with_modules/4.1.2-23080815/Dockerfile)</sup> |
| [samtools](https://github.com/samtools/samtools) | [LICENSE](https://github.com/samtools/samtools/blob/1.17/LICENSE) | [1.17](https://ghcr.io/tgen/containers/samtools)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/samtools/1.17-23080815/Dockerfile)</sup> |
| [samtools_python](https://github.com/samtools/samtools) | [LICENSE](https://github.com/samtools/samtools/blob/1.17/LICENSE) | [1.17](https://ghcr.io/tgen/containers/samtools_python)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/samtools_python/1.17-3.7.16-23082819/Dockerfile)</sup> |
| [sigprofiler](https://github.com/AlexandrovLab/SigProfilerAssignment) | [LICENSE](https://github.com/AlexandrovLab/SigProfilerAssignment/blob/main/LICENSE.txt) | [0.0.24](https://ghcr.io/tgen/containers/sigprofiler)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/sigprofiler/0.0.24-23080710/Dockerfile)</sup> |
| [sigprofiler](https://github.com/AlexandrovLab/SigProfilerAssignment) | [LICENSE](https://github.com/AlexandrovLab/SigProfilerAssignment/blob/main/LICENSE.txt) | [0.0.24](https://ghcr.io/tgen/containers/sigprofiler)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/sigprofiler/0.0.24-24030411/Dockerfile)</sup> |
| [snpsniffer](https://github.com/tgen/snpSniffer) | [LICENSE](https://github.com/tgen/snpSniffer/blob/v7.0.0/LICENSE) | [7.0.0](https://ghcr.io/tgen/containers/snpsniffer)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/snpsniffer/7.0.0-23080810/Dockerfile)</sup> |
| [strelka](https://github.com/Illumina/strelka) | [LICENSE](https://github.com/Illumina/strelka/blob/v2.9.10/LICENSE.txt) | [2.9.10](https://ghcr.io/tgen/containers/strelka)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/strelka/2.9.10-23080711/Dockerfile)</sup> |
| [thred](https://github.com/tgen/tHReD) | [LICENSE](https://github.com/tgen/tHReD/blob/main/LICENSE) | [1.1.0](https://ghcr.io/tgen/containers/thred)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/thred/1.1.0-23080712/Dockerfile)</sup> |
| [transparser](https://github.com/tgen/transParser) | [LICENSE](https://github.com/tgen/transParser/blob/master/LICENSE) | [1.0.1](https://ghcr.io/tgen/containers/transparser)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/transparser/1.0.1-23080810/Dockerfile)</sup> |
| [trinity_bwa_mem2](https://github.com/trinityrnaseq/trinityrnaseq) | [LICENSE](https://github.com/trinityrnaseq/trinityrnaseq/blob/v2.8.6/LICENSE) | [2.8.6_2.2.1_1.17](https://ghcr.io/tgen/containers/trinity_bwa_mem2)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/trinity_bwa_mem2/2.8.6-23082819/Dockerfile)</sup> |
| [vcfmerger2](https://github.com/tgen/vcfMerger2) | [LICENSE](https://github.com/tgen/vcfMerger2/blob/v0.9.4/LICENSE.md) | [0.9.4](https://ghcr.io/tgen/containers/vcfmerger2)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/vcfmerger2/0.9.4-23080809/Dockerfile)</sup> |
| [vcfmerger2](https://github.com/tgen/vcfMerger2) | [LICENSE](https://github.com/tgen/vcfMerger2/blob/v0.9.5/LICENSE.md) | [0.9.5](https://ghcr.io/tgen/containers/vcfmerger2)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/vcfmerger2/0.9.5-23090616/Dockerfile)</sup> |
| [vcfmerger2](https://github.com/tgen/vcfMerger2) | [LICENSE](https://github.com/tgen/vcfMerger2/blob/v0.9.5/LICENSE.md) | [0.9.5](https://ghcr.io/tgen/containers/vcfmerger2)<sup>[Dockerfile](https://github.com/tgen/containers/blob/main/vcfmerger2/0.9.5-23090712/Dockerfile)</sup> |
