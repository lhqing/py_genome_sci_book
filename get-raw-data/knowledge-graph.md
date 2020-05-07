# Stages of Genome Data Generation

Regardless of what technology or what programming langue you care about, let's discuss some principles of genome data generation first. I will not talk about the routine processing in the later chapters. Everything here is just making sure you understand how the "raw input" files is generated before python based analysis.

## Stage I - Understand the Technologies

Almost every month, the CNS, Nature Methods, and Nature Biotechnology will publish some papers that report "new sequencing technologies" for specific purposes. Although we could easily name hundreds of sequencing technologies today, they are not that different. 

Here I try to organize them in two ways. Once having the organization in mind, you won't be afraid of the tons of "new terms" you met in genomic papers. They eventually based on things mentioned below:

{% tabs %}
{% tab title=" Organization via Biological Question" %}
![](../.gitbook/assets/image%20%2818%29.png)

### Organization via Biological Question

This nice plot comes from [**the ENCODE project**](https://www.encodeproject.org/), a project about building encyclopedia of DNA elements. Based on this plot, here are some technologies worth remembering:

* **Transcriptome: RNA-seq** \(and its numerous variations focusing on [different parts of the transcriptome](https://www.thermofisher.com/us/en/home/life-science/sequencing/sequencing-education/next-generation-sequencing-basics/rna-sequencing-methods.html), here is a [video](https://www.youtube.com/watch?v=tlf6wYJrwKY)\)
* \*\*\*\*[**Epigenome**](https://www.youtube.com/watch?v=Tj_6DcUTRnM):
  * **Protein - DNA interaction: ChIP-seq** \(using antibody targeting transcription factor, to study where that protein bind to DNA, here is a [video](https://www.youtube.com/watch?v=nkWGmaYRues)\)
  * **Histone modification: Also ChIP-seq** \(using antibody targeting specific histone modifications, here is a [video](https://www.youtube.com/watch?v=nkWGmaYRues)\).
  * **DNA methylation: WGBS-seq** \(using a chemical called bisulfite to create artificial DNA mutations that representing unmethylated cytosine in DNA. It studies the DNA methylation status through detecting these mutations. My lab published the first [human bulk WGBS-seq paper in 2009](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2857523/), and studying DNA methylation is also my main project - but now at the single-cell level.\)
  * **Chromatin accessibility: ATAC-seq** \(using a Transposes called Tn5 that can insert a DNA fragment with specific adapter sequences into open regions of the DNA to break it, then sequence those fragments with the adapter to get the open information. Open means active. Here is a [video](https://www.youtube.com/watch?v=TXzOXUl0g5Q)\).
* **Genome**: Just sequencing the **DNA sequence itself** to identify mutations compared to the reference genome. This includes **whole genome sequencing** and **exon-seq**. The later use a fluid chip to capture exon region DNAs to only sequence this 2% of the genome only, representing a category of money-saving technologies called targeted sequencing.
{% endtab %}

{% tab title="Organization via Coverage Or Mutation" %}
![Schematic of Reads Profiles in Each Main Technology  ](../.gitbook/assets/image%20%2824%29.png)

### Organization via Coverage Or Mutation

We can regroup the leading technologies into two categories: 

1. These technologies care about **coverage at particular genome locations \(RNA-seq, ATAC-seq, ChIP-seq, HiC\)**. They are different in that **their reads come from different types of features in the genome** -- due to various treatments during library preparation. Analysis related to these technologies can also be aggregated into these categories: 
   * Determine whether a particular region has more reads than the background noise -- active/expressed or not
   * In a specific region, determine whether reads number in one sample is different from the other sample \(such as differentially expressed gene analysis\)
   * De-novel determination of new genome features. For example, we can define or refine gene annotation using the RNA-seq.
2. These technologies care about **the actual sequence and mutation of the sequence \(genome-seq, exon-seq, WGBS-seq\)**. Coverage information is also vital because high coverage means high confidence. However, coverage is not the final output of these technologies. The final output is **the fraction of reads with mutation compare to the total covered reads in the same genome locus**. Analysis related to these technologies can be summarized as:
   * Confidently determine real mutations over technical errors in sequencing. A.K.A. Call Variants.
   * For specific mutation, compare whether it more frequently occurs in one sample versus the other samples.
{% endtab %}
{% endtabs %}

## Stage II - Library Preparation

The library preparation is the most diverse stage among different technologies. Most new technology papers are indeed talking about new ways of preparing library, which allow them to 

* Sequencing a **different subset** of the genome, epigenome, or transcriptome, to study specified biological questions. For example, total RNA-seq sequencing sequence all the RNA molecules, poly-A captured RNA-seq sequencing mRNAs. 
* **Multiplexing** different samples or cells together via adding barcode sequences to the ends of DNA fragments. This is a critical step in single-cell sequencing, but also common in bulk-seq. Fancy barcoding techniques can multiplex [hundreds of thousands of cells in one experiment](https://science.sciencemag.org/content/360/6385/176).
* Increasing throughput, efficiency, decreasing cost, etc.

### The additional sequence added onto the original DNA fragment

One of the primary purposes of library preparation is adding additional sequences to your input DNA fragments:

* **Adapter**: during library preparation, there must be a step adding adapter sequences to the ends of DNA fragments. Only DNA fragments with adapters can be captured by complementary adapters on the Illumina flowcell, thus being sequenced. The adapters can be added via ligation or PCR. 
* **Barcode**: The barcode is the predefined sample-specific sequence incorporated into somewhere \(usually in conjunction with the adapter\) in the DNA fragments during library preparation. The barcode is used to distinguish different samples, reads with the same barcode will be assign to the same sample. It's used in almost all sequencing experiments because usually, single sample does not fulfill the capacity of the Illumina machine. We need to **multiplex** samples' DNA fragments together to sequence them. The barcodes can be added via ligation or PCR. 

These artificial sequences must be removed before you start any biological analysis, see stage IV.

{% hint style="info" %}
To give you a feeling of adapter and barcodes, below is the read structure from [technology used in my project](https://www.nature.com/articles/s41467-018-06355-2). No need to understand the details, but do notice that:

* Only the gray part in the middle is actual DNA fragment \(~120 bp\) contains biological information
* The colored regions \(~30bp in total\) are used for amplifying genome DNA, barcodes, and adapter sequences.
* The library preparation is all about adding those parts onto DNA fragments via PCR and ligation.
* We then use the barcode information to demultiplex samples and remove all of them before further analysis.
{% endhint %}

![](../.gitbook/assets/image%20%288%29.png)

### The fragment length

The Illumina sequencer requires input DNA fragments having similar lengths, which is usually selected via magnetic beads \(see this [video](https://www.youtube.com/watch?v=zGV0SjCe0CU)\). Each library has a fragment length distribution. They must be measured and reported together with the sequencing data.

## Stage III - Sequencing

### Illumina Sequencing by Synthesis

[This GREAT video](https://www.youtube.com/watch?v=fCd6B5HRaZ8&t=1s) visualizes the Illumina sequencing, explains why the adapter is needed and what is pair-end sequencing.

### Pair-end sequencing

Pair-end sequencing is most common nowadays. The above video explained how Illumina machine uses end-specific adapter and bridge PCR to sequence both ends of the DNA fragments, which gives you two fastq files called "R1" and "R2".

#### Fragments vs Reads

We call the single read \(either R1 or R2\) a read, and we call paired R1 and R2 a fragment because they should represent the original input DNA fragment. Whether R1 and R2 are overlapped depends on your read length and DNA fragment length.

![](../.gitbook/assets/image%20%2816%29.png)

{% hint style="info" %}
In addition to illumina sequencing, the third generation sequencing will become popular in coming years. I do want to start learning those, with a real project, some times later, but I will not talk about them in this book.

Check out the two fancy technologies [NANOPORE](https://www.youtube.com/watch?v=E9-Rm5AoZGw) and [PacBio](https://www.youtube.com/watch?v=_lD8JyAbwEo) of 3rd generation sequencing.
{% endhint %}

## Stage IV - Process Raw Reads

### The BCL file

The BCL file is indeed the raw file produced by the sequencer. A sequencer is just a **camera machine** taking thousands of photos of the flowcell. The **BCL file contains raw base calls from the images**. The FASTQ file is generated from the BCL file with a software called [Bcl2fastq](https://support.illumina.com/sequencing/sequencing_software/bcl2fastq-conversion-software.html) provided by the Illumina. It does two things:

* Generate the reads with their base quality score from the BCL file, output FASTQ format.
* **Demultiplex** samples from the same sequencing run using the barcode information.

Usually, this step is done by the service provider; you don't need to do that. And BCL file is larger than the FASTQ file, so not used for data transfer.

### The FASTQ file

The raw fastq file usually needs to be cleaned. An excellent tool to profile and monitor the cleaning process is the [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/download.html), and the standard tool for actual cleaning is the [cutadapt](https://cutadapt.readthedocs.io/en/stable/). For mature sequencing technologies, using [trim\_galore](https://www.bioinformatics.babraham.ac.uk/projects/trim_galore/) is a good option to save your time. Usually, the trimming and filtering steps only remove small portion \(likely &lt; 10%\), if you lost lots of reads after this step, something must went wrong in the sequencing.

{% hint style="info" %}
We call the bcl2fastq output FASTQ files unprocessed raw files, which is the one needed by GEO for publication related data sharing. In the raw FASTQ files:

* All reads should have the same length
* R1 and R2 files should have the same number of reads
* Paired reads occur with same order in R1 and R2 files
{% endhint %}

### Trim and filtering

The usual FASTQ file QC includes:

* removing low-quality bases, if the quality score is low, that base call might introduce artificial mutation, impact mapping rate and further analysis
* removing additional barcode and adapters, they might not be recognized fully by bcl2fastq if there are technical errors. 
* Filtering reads that are too short after the above two steps.

{% hint style="info" %}
All the adapter and barcode sequences must be removed from your reads before mapping. They are artificial.
{% endhint %}

{% hint style="info" %}
For most cases, R1 & R2 files need to be processed together. For pair-end mapping, if R1 is filtered out, so does R2. After this, the R1 R2 still have the same number of reads and the same read order.
{% endhint %}

## Stage V - Give the reads a location \(Alignment or Mapping\)

After getting the clean FASTQ files, the next stage is to give your reads location information, a.k.a mapping/alignment. These two words were interchangeable, until a special type of mapper for RNA-seq been developed a few years ago \([Kallisto](https://pachterlab.github.io/kallisto/) or [Salmon](https://combine-lab.github.io/salmon/)\). So now, things differ as follow:

```python
# how to give your reads a location

if has_reference_genome:
    if rna_seq:
        if has_reference_gene_annotation:
            if only_care_about_transcript_abundance:
                run_kallisto() # or run_salmon()
            else:
                # you care about the actual genome location
                # you want the BAM file for genome browser and other purpose
                # you want to define posible noval splicing variants
                run_star()
                # and you need to run other feature counts softwares bellow
        else:
            # no reference gene annotation, not covered in this book
            run_de_noval_transcriptome_assembly()
    else:
        # all other technologies, DNA-seq, epigenomic-seq
        # run_bwa(), run_bowtie(), run_bowtie2(), run_hisat2() ...
        run_one_of_the_aligner()
else:
    # no reference genome, not covered in this book
    run_de_noval_genome_assembly()
```

### The SAM/BAM format

Except for Kallisto and Salmon that do not provide you genome location and mismatch information, all other aligners will produce SAM/BAM files. Key points are:

* The FASTQ file contains the named reads with their sequence and sequence base quality. 
* The SAM file contains **everything from the FASTQ file** plus **genome location** information and **mismatch** information. 
* The BAM file is a binarized and compressed version of SAM. 
* The BAM file is better for data storage and further analysis.

### SAM/BAM QC

SAM/BAM file also needs QC, mainly:

* Remove PCR duplicates.
* Remove non-uniquely mapped reads.

Both doable via Samtools, as [explained later](../genome-science/data-formats/sam-bam.md).

{% hint style="info" %}
Kallisto does generate genome BAM file for genome browser [if needed](https://pachterlab.github.io/kallisto/manual).
{% endhint %}

### The Reference

It is VERY IMPORTANT to keep track of your reference genome and your gene annotation **version**. I created a standalone reference directory in my home directory `~/ref/` with its subdirectories organized by species and data sources. And I recorded every change I made in that directory. All informations will go into the methods section of my paper.

{% hint style="info" %}
Never make custom changes to any reference files; consistency is the key to the mental health of bioinformaticians.
{% endhint %}

## Stage VI - Get the processed "raw" data from located reads

Processed raw data refer to the direct input of custom analysis using python. It is technology-specific:

* For RNA-seq, the processed raw data is "read counts in each gene/transcript of each sample", without any normalization or filtering
* For ATAC-seq and ChIP-seq, the processed raw data can be just the BAM file, because there is usually no "reference annotation" for regulatory elements, we just de novo define the regulatory elements \(a.k.a. peaks\) via the reads coverage.
* For HiC, the processed raw data are BEDPE. It records two genomic regions in a bed-like format, representing two anchors of the DNA-DNA interaction.
* For mutation-based technologies \(genome-seq, exon-seq, and WGBS-seq\), there is a standard format called VCF/BCF, but WGBS-seq usually uses other lightweight custom table formats. Nevertheless, the information in processed raw data is "number of reads having the mutation \(numerator\) and total number of reads \(denominator\) in the same genome loci". 

Unlike FASTQ and SAM/BAM format, the processed data are usually in custom CSV/TSV format \(except the VCF format\) or just a data matrix in an [HDF5 file](https://en.wikipedia.org/wiki/Hierarchical_Data_Format). This is where python comes in to help. You need to start writing your own code finally!

## How to choose among tools?

The quick answer is don't spent too much time choosing similar tools. As long as you are not writing a technical benchmarking paper, they are not that different. Find a highly cited paper that used the same technology as you do and use whatever they use, with same parameters.

## Do not reinvent the wheels

If you are new to genome science, remember that the analysis infrastructure for most common sequencing technologies is rather mature. If you feel like any step during preprocessing needs you to write a bunch of custom code to accomplish, that usually means you haven't found the right tool. Try search Pubmed, google, and youtube first.

![](../.gitbook/assets/img_0240.jpeg)

