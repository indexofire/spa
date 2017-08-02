## 2. Public Database Isolates

### 2.1 Get Data

```bash
# 使用edirect工具生成适合的 SRA 信息列表
$ esearch -db 'SRA' -query 'txid54388[Organism:exp] AND (cluster_public[prop] \
> AND "biomol dna"[Properties] AND "strategy wgs"[Properties])' | \
> efetch -format runinfo > SPA.cvs

# 可以使用excel等工具来过滤不需要的数据，如数据量过小的数据，测序平台仅为
# hiseq, miseq, nextseq 的数据.
# 这里用 awk 来实现，最后获得261个复合的测序SRA数据，使用 prefetch 工具下载
# prefetch下载建议单线程即可，如果ascp速度仍旧不够，可以尝试在EBI的FTP上下载
$ awk -F',' '{if ($20~/MiSeq/ || $20~/HiSeq/ || $20~/NextSeq/) \
> print $1}' < SPA.csv > illumina_SPA.csv
$ grep -i '^[DES]RR' illumina_SPA.csv | xargs prefetch -v
```

### 2.2 Convert File Format

```bash
# 把 sra 格式的数据转换成 fastq 格式
$ mkdir -p ../fastq
$ parallel "fastq-dump --split-files --gzip --outdir ../fastq" ::: *.sra

# 部分数据可能是 se 或者 matepair 的文库，后面拼接采用的方式不同，因此放到不同文件夹
$ mkdir -p ../fastq/pe
$ mkdir -p ../fastq/se
$ cd ../fastq && ls -l *.fastq.gz | awk -F'_' '{print $1}' \
> | awk '{print $9}' | uniq -u
ERR1056308

# ERR1056308 为 se 文库测序数据，其余为 pe 文库测序数据，将其分别放置到相应文件夹中。
$ mv ERR1056308_1.fastq.gz se
$ mv *.fastq.gz pe
```

### 2.3 Check Quality
