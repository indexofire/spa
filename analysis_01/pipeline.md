## 1. Local Isolates Sequencing Result

### 1.1 check the quality

```bash
# make all sample's ngs fastq.gz file to subdirectory and use fastqc to check
# the quality of sequencing result
$ for i in $(ls *.fastq.gz | awk -F'_' '{print $1}'); \
> do mkdir -p $i && mv ${i}_*.fastq.gz $i; \
> do fastqc -o ${i}/00_fastqc --extract -f *.fastq.gz -t 40 -q; \
> done
```

```bash
# Assemble samples
$ for i in $(ls -D); do spades.py -k 21, 33, 55, 77 -pe -1 \
> ${i}/${i}_1.fastq.gz -2 ${i}/${i}_2.fastq.gz \
> --cov-cutoff -t 40 -o ${i}/assembly
```
