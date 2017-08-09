# 杭州地区Salmonella paratyphi A基因组分子流行特征研究

## 研究一 杭州地区S. Paratyphi A 菌株特征分析

### 1\. 实验方法

**1.1 基因组测序：** 选择200 - 200 年杭州地区甲型副伤寒沙门菌分离株共 送用 Qiagen Mini DNA Kit 提取基因组DNA，送华大进行基因组测序。测序平台为 Hiseq 2500，测序方式为 PE150。对测序数据用 FastQC[1] 进行质控并用 Trimmomatic[2] 去除低质量序列和接头。用 pavian[3] 扫描短序列以确定外源DNA污染程度。用 spades[4] 对质控后数据进行基因组拼接。

**1.2 基因组扫描：** 用 srst2[5] 对短序列测序数据进行扫描获得 MLST 型别和毒力基因与耐药基因序列。对 fasta 格式的拼接序列用 mlst_check[6] 扫描获得各个菌株 ST 型别。用 sistr_cmd[7] 工具扫描拼接序列，获得其血清型别和 cgmlst 型别。

* [1] <https://www.bioinformatics.babraham.ac.uk/projects/fastqc/>
* [2] Bolger, A. M., Lohse, M., & Usadel, B. (2014). Trimmomatic: A flexible trimmer for Illumina Sequence Data. Bioinformatics, btu170.
* [3] Florian P Breitwieser, ProfileSteven L Salzberg. Pavian: Interactive analysis of metagenomics data for microbiomics and pathogen identification. doi: <https://doi.org/10.1101/084715>
* [4] Nurk S, Bankevich A, Antipov D, et al. Assembling single-cell genomes and mini-metagenomes from chimeric MDA products. J Comput Biol. 2013,20(10):714-37.
* [5] Michael I, Harriet D, Lesley-Ann R, et al. SRST2: Rapid genomic surveillance for public health and hospital microbiology labs. Genome Medicine,2014, 6:90
* [6] "Multilocus sequence typing by blast from de novo assemblies against PubMLST", Andrew J. Page, Ben Taylor, Jacqueline A. Keane, The Journal of Open Source Software, (2016). doi: <http://dx.doi.org/10.21105/joss.00118>
* [7] Catherine Yoshida, Peter Kruczkiewicz, Chad R. et al. The Salmonella In Silico Typing Resource (SISTR): an open web-accessible tool for rapidly typing and subtyping draft Salmonella genome assemblies. PLoS ONE 11(1): e0147101.

### 2\. 实验结果

**2.1 基因组测序**

## 研究一 S. Paratyphi A Pan-genome 研究

下载 NCBI SRA 数据库中 S. Paratyphi A 血清型的测序数据。使用 FastQC 质控，用 Trimmomatic 去除接头和低质量序列片段。用 spades 进行基因组拼接，用 SISTR 扫描确认血清型，并且活动相应 cgmlst 型别。下载 Assembly 数据库中 S. Paratyph A 血清型基因组拼接数据。将 SRA 和 Assembly 数据库的数据合并，最后确认有 株甲型副伤寒沙门菌基因组数据。

## 研究二 杭州地区S. Paratyphi A 菌株特征分析

杭州地区甲型副伤寒沙门菌基因组测序。提取杭州地区甲型副伤寒沙门菌基因组核酸，送华大基因进行高通量测序。测序平台为Hiseq2500，测序模式为PE150。使用FastQC质控，用Trimmomatic去除接头和低质量序列片段。用spades进行基因组拼接，用SISTR扫描确认血清型。

## 研究三

从Enterbase数据检索血清型符合S. Paratyphi A的记录，将SISTR复核基因组中血清型有疑问的记录去除，共获得1060条记录。
