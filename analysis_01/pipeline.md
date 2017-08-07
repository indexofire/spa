## 1. Local Isolates Sequencing Result

### check the quality

```bash
# make all sample's ngs fastq.gz file to subdirectory and use fastqc to check
# the quality of sequencing result
$ for i in $(ls *.fastq.gz | awk -F'_' '{print $1}'); \
> do mkdir -p $i && mv ${i}_*.fastq.gz $i; \
> do fastqc -o ${i}/01_fastqc --extract -f *.fastq.gz -t 40 -q; \
> done
```

### assembly data

```bash
# Assemble samples
$ for i in $(ls -D); do python2 /usr/local/bin/spades.py --careful \
> -k 33,55,77 -1 ${i}/00_raw_data/${i}_1.fastq.gz \
> -2 ${i}/00_raw_data/${i}_2.fastq.gz --cov-cutoff 10.0 -t 40 \
> -o ${i}/02_assembly; done
$ for i in $(ls -D); do cp ${i}/02_assembly/scaffolds.fasta \
> ../assemblies/HZ_${i}.fasta; done
```

### serovar check

```bash
$ cd assemblies
$ for i in *.fasta; do sistr --qc -vv --alleles-output allele-result.json \
> --novel-alleles novel-alleles.fasta --cgmlst-profiles cgmlst-profiles.csv \
> -f tab -o ${i}.tab $i; done
```

### MLST check

```bash
# Use assembly to check
$ mlst --scheme salmonella *.fasta > result.txt
# Use fastq to check
$ for i in $(ls -D); do srst2 --input_pe ${i}/00_raw_data/{$i}_R1.fq.gz \
> ${i}/00_raw_data/${i}_R2.fq.gz --output ${i}/03_mlst/ --log \
> --mlst_definitions salmonella.txt --mlst_db Salmonella_enterica.fasta \
> --mlst_delimiter _; done
```
