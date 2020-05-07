# BAM to FASTQ

SAM/BAM format contains both reads information and the mapping information. Sometimes when you may want to extract the reads information from a SAM/BAM file to remap it. Some mapping softwares \(e.g. Salmon\) also take the the SAM/BAM file directly so the you can skip the extraction step. But if you do have to do so, you can use [`bedtools bamtofastq`](https://bedtools.readthedocs.io/en/latest/content/tools/bamtofastq.html)\`\`

```text
# single end
bedtools bamtofastq [OPTIONS] -i <BAM> -fq <FASTQ>

# pair end
bedtools bamtofastq -i aln.qsort.bam \
                      -fq aln.end1.fq \
                      -fq2 aln.end2.fq
```



