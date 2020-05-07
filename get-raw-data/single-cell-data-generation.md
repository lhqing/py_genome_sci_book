---
description: This page is about single-cell sequencing
---

# From Bulk To Single Cell

## What is single-cell sequencing?

Single-cell sequencing is a huge technology advance compare to bulk-seq. Instead of using a whole tissue as the bulk-seq did, it aims to **detect different kinds of molecular information at the single-cell level.** 

The most common type of single-cell sequencing is the **single-cell RNA-seq** \(scRNA-seq\), and the most available scRNA-seq method is called [10X Chromium](https://www.10xgenomics.com/products/single-cell/?src=search&lss=google%20genomics%20Genomics&cnm=sem-goog-2020-website-page-ra_g-p_brand-amr-retarget&cid=7011P000000oWys). This mature technology is run by a company called 10X genomics. When technology is commercialized by a company, it can easily beat other technologies developed and maintained in research labs due to its much user-friendly supports. Another scRNA-seq technology worth remembering is called [SMART-seq](https://www.nature.com/articles/nprot.2014.006).

{% hint style="info" %}
A simple summary of the difference between these two is: In each single experiment, SMART-seq sequence **full-length RNA** in **fewer cells** with **deep coverage in each cell** while 10X sequence **3' of RNA molecule only** in **more cells** with **lower coverage** in each cell.
{% endhint %}

The epigenomic field also went into the single-cell era right after the transcriptomics. The most mature epigenomic technologies that have been adapted into single-cell form are **ATAC-seq \(also supported by 10X now\)** and **WGBS-seq \(DNA methylation\)**. And we also saw **HiC** been applied on the single-cell level in [a few studies](https://scholar.google.com/scholar?hl=en&as_sdt=0%2C5&q=single+cell+chromatin+contacts&btnG=). The **ChIP-seq**, although pivotal to epigenomics, hasn't been applied on a **large scale** at the single-cell level \([Prove of concept studies](https://scholar.google.com/scholar?hl=en&as_sdt=0%2C5&q=single+cell+chip+seq&btnG=&oq=single+cell+chip+) do exist, and I am sure this will be changed in the future\).

All in all, the take-home message is that most kinds of bulk sequencing can somehow be adapted to perform at single-cell level. The contents below talk about how this is realized conceptually. For all the technical details, I suggest you read the original papers if you are interested, or there are many great seminar videos on YouTube. 

## Why single-cell?

In my opinion, all the advantages of single-cell sequencing technologies can be summarized as **giving you the ability to understand cellular heterogeneity in a much higher resolution**. Single-cell technology does not solve all the problems but is already much better comparing to previous studies. When I read those early bulk-seq papers published before 2015, I sometimes saw people treating the words "tissue" and "cell type" as the same, and even for the complex brain, only two cell types mattered, the neurons and non-neurons. Recently, my collaborators and I [reported dozens of clusters from a piece of the mouse brain](https://www.biorxiv.org/content/10.1101/2020.02.29.970558v2). Although whether all these clusters can be called "cell types" remain to be a hot debate, the standard of discussing cellular heterogeneity has been greatly elevated by single-cell technologies.

Once we can separate everything, we can easily regroup them together - into a level that is most convenient for discussing particular biological questions. Just like this common metaphor below:

![Single cell on the left, bulk on the right \(all juices are mixed from multiple kinds of fruits\)](../.gitbook/assets/image%20%2828%29.png)

## How to get single cells?

### Plate-based or bead-based

The first step of single-cell sequencing is to isolate single cells. In the earliest low-throughput studies, individual cells were manually picked up after dissociation. Today, most technology uses one of the two strategies: 1. Distribute single or multiple cells into each well of a plate, 2. Using microfluidic devices to separate individual cells with oil drop.

The plate-based technology can be both medium-throughput or high-throughput. The SMART-seq is the representative of medium-throughput scRNA-seq methods, where we usually sort single cells into each well of the 384 plates, and the number of wells is the upper limit of the number of cells in each experiment. Alternatively, one can sort multiple cells into a single well, and use some [cleaver barcoding technology](https://science.sciencemag.org/content/360/6385/176) \(see below\) to barcode most of the cells differently, thus reaching a much higher throughput. Another way to achieve high throughput is by using special micro-well plates, having thousands of wells in each plate, thus increasing the cell number. Two technologies used the micro-well strategy \([microwell-seq](https://www.ncbi.nlm.nih.gov/pubmed/29474909) or [seqwell](https://www.nature.com/articles/nmeth.4179)\) for scRNA-seq.

The bead-based technology is high throughput, and the representative methods are the 10X and drop-seq. This [video ](https://www.youtube.com/watch?v=vL7ptq2Dcf0)from drop-seq authors clearly explained how microfluidic technique is used to control single barcoded bead and single cell to mix in an oil drop. In principle, 10X is similar to this. 

{% hint style="info" %}
In a single experiment, low throughput means 10 - 100 cells; medium throughput means 300 - 3000 cells; high throughput means 3000 - 100,000 cells
{% endhint %}

### Cells or nuclei

Sometimes, you might saw me or other papers describing their technology as single-nuclei rather than single-cell. This is because for some tissues, such as the brain, dissociating single cells is very hard and can cause cross-contamination between cells; dissociating single nuclei is much easier. Indeed, many brain studies I've seen using nuclei but not cells, and still get excellent resolution. For epigenomic studies, everything should happen in the nuclei anyway, so we don't lose anything.

I do not distinguish single-cell or single-nucleus on this page.

## How to prepare the single-cell library?

For plate-based technologies, usually a liquid handler \(a.k.a. pipetting robot?\) is needed. This is[ the one](https://www.beckman.com/liquid-handlers/biomek-i7) we currently use. All it does is pipetting liquids based on preset programs, automatically make thousands of PCR-like reaction in the wells of the plates. [Watching it work](https://www.youtube.com/watch?v=xNEP-yzwbRE) is a good mind relaxing activity until bug shows up. Setting up this kind of machine needs time and specialized person, therefore not that easy for most labs and preventing general biology labs from doing it. Collaboration with a genomic lab is usually needed.

For commercialized bead-based technologies, doing library preparation is reasonably easy for everyone. For 10X, it only takes half an hour to [prepare the library](https://www.youtube.com/watch?v=sgzI8el4ykM) on a single fully automatic machine - another reason 10X become so popular.

## How to index single cells with barcodes?

In the [previous page](knowledge-graph.md#the-additional-sequence-added-onto-the-original-dna-fragment), I mentioned that the main purpose of library preparation of Illumina sequencing is to add adapters and barcodes onto the DNA fragments. Same thing here for single-cell technologies. Most bulk-seq studies only have several to dozens of samples. However, for single-cell experiments, **each cell is a "sample"**, and we profile hundreds of thousands of them in one experiment. Therefore, we need more complex barcodes to increase its capacity and decrease the [**collision rate**](single-cell-data-generation.md#collision-rate).

Most technical papers about scRNA-seq are talking about how we can index more cells in a single experiment or how this can be made more efficient so that we can detect more genes per cell. For medium-throughput technologies, barcoding is very similar to bulk-seq. For high throughput technologies, I use two examples, one from 10X, the other from [Split-seq](https://science.sciencemag.org/content/360/6385/176). Understanding these two strategies can then help understand most of the other technologies.

### Medium throughput strategy

For those plate-based medium-throughput technologies, because every well only has one cell, we can put unique barcode in each well, and index the cell much like what bulk-seq does. A [fully automated liquid handler](single-cell-data-generation.md#how-to-prepare-library-at-single-cell-level) can easily achieve this.

### 10X's barcode strategy

![https://www.10xgenomics.com/products/single-cell/](../.gitbook/assets/image%20%2811%29.png)

10X is bead-based method \([video](https://www.10xgenomics.com/products/single-cell/?src=search&lss=google%20genomics%20Genomics&cnm=sem-goog-2020-website-page-ra_g-p_brand-amr-retarget&cid=7011P000000oWys)\). On the surface of each gel bead from the 10X reagent, millions of single-strand oligo were pre-synthesized. During 10X library preparation, a single cell will be grouped with a single bead inside an oil drop, the RNA molecules from that cell will be captured by the oligo on the bead surface, via poly\(dT\) or specific capture sequence. In addition to the capture sequence, these oligos also contain two kinds of barcodes - the 10x barcode and the UMI.

* **10x barcode** is bead specific, which means all oligos in the same bead have the same 10x barcode. And because each bead is paired with one cell, the 10x barcode is the **cell's identity barcode**.
* **UMIs** \(unique molecule index\) are random sequences, approximately unique to every oligo. UMI is the **ID of a single RNA molecule**, because one oligo can only capture one RNA molecule.

These barcodes will be part of the reverse-transcribed cDNA. After breaking the oil drop and mixing all the cDNA fragments together, the remaining steps are just like preparing the normal RNA-seq library. And during the sequencing step, R1 will read through all these barcodes information, R2 will read through the actual RNA sequence. Thus, we can use the 10x barcode, and UMI sequence from R1 to group reads back into each cell, and use the R2 RNA sequence to tell which gene this read from.

### Split-seq strategy

![SPLiT-seq](../.gitbook/assets/image%20%2817%29.png)

The plate-based [SPLiT-seq](https://science.sciencemag.org/content/360/6385/176) uses a different approach to reach high throughput: 

1. Split multiple cells into each well, and introduce first barcode via reverse transcribe primer. Cells in the same well do get the same barcode. 
2. Pool all the cells together, and randomly re-split it into another plate. In the new plate, introduce another set of barcodes via ligation. Cells in the same well also get the same barcode.
3. Repeat step2 for three times.
4. The final fragments from a cell contain four round of barcodes, and because every split-pool is random, it is unlikely that two cells will always stay together in the same well and getting the same barcodes.

### collision rate

Collision refers to a bad situation when two \(or more\) cells got the same barcode sequence. Therefore, we can not distinguish them from the sequencing reads, nullify data for both cells. All the high throughput barcoding strategies potentially suffer from this problem. Because there is no careful handling of single cells, every step is random and based on the calculation from poison distribution.

In theory, there are two ways to decrease the collision rate. The first way is to increase the barcode complexity. Longer barcodes can have exponentially more combinations. The other way is controlling the cell concentration; for example, in 10X, the number of gel beads is much more than the number of cells. Thus, it is less likely that two cells will got the same beads.

In practice, we have a standard way to evaluate the collision rate, which is using the technology to sequence a cell population that's mixed from human \(50%\) and mouse \(50%\) cells. We then map the reads to both human and mouse genomes. Because these are two different species, reads from either a single human cell or mouse cell can only map to the corresponding genome, reads from a human-mouse colliding cell are partially mappable to both genomes. The later case gives us an estimation on the collision rate.

![A typical human mouse collision plot ](../.gitbook/assets/image%20%2830%29.png)

Red or blue dots are cells only mappable to human or mouse genome, the gray dots are partially mappable to both, therefore, very likely due to collision.

{% hint style="info" %}
In real data, collision also exists. There is a kind of computational analysis called "doublets removal" that deals with this problem.
{% endhint %}

## Single cell Data

![Minimum basic data analysis for scRNA-seq](../.gitbook/assets/image%20%284%29.png)

### Sequencing data

Although the single-cell preparing steps are very different from bulk-seq, the Illumina sequencing and preprocessing steps are very similar. Most existing software can be directly used to QC, filter, map, and count the reads. Read-level single-cell data also use consistent data format as the bulk-seq does. The most significant difference is the sample number. In single-cell sequencing, you easily get hundreds of thousands of samples \(cells\). Usually, we do not save separate files for each cell, but use integrated file formats for the whole dataset. [Mature pipeline](https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/what-is-cell-ranger) exists for standard technologies like 10X.

### Processed Raw Data

For scRNA-seq, the processed data is a cell by gene raw count table. This table is much like when you summarize all your bulk-seq samples' gene counts together. But one thing that's unique to single-cell data is that this table is usually **sparse**. Because coverage of every single cell is much less than bulk-seq, so many zeros in the matrix might be due to low coverage rather than no expression. Many computations performed on single-cell level need to take this into consideration.

### Clustering or Trajectory Analysis

Clustering analysis based on the hypothesis that your cell population is composed of multiple cell types, and you are more interested in the difference between cell types rather than within cell types. The tricky part for clustering analysis is to **determine the cluster numbers**. This problem does not have ground truth, and people use different criteria to solve it. For simple situations such as Peripheral Blood Mononuclear Cells, clusters can be easily matched with known cell types. But for complex tissue such as the brain, annotating clusters into cell types is still very hard to reach consensus. More functional experiments are needed to help us understand those computationally determined clusters.

[Trajectory analysis](https://www.nature.com/articles/s41587-019-0071-9) provides a complementary view of the data; it emphasizes the continuous change in the cell population rather than requiring clear categorical borders. Datasets more suitable for trajectory analysis are likely coming from developmental or time-series experiments \(see these [beautiful results](https://science.sciencemag.org/content/360/6392/eaar3131?casa_token=pvr25EmR8AsAAAAA:owYVNYX7iQKqEVBYLppBP_LOAS5U1TbHKN_aJp-qEEgg--QXmDH7jLeFomPXV08w32gsModqpOs_) for zebrafish development\), where understanding what genes are changed/correlated with the continuous trajectory is more important. Another situation that may need this continuous view is the intra-cell-type gradients. This situation is especially evident in the brain, where spatial gradients exist in well-defined cell types.

![Trajectory and clustering analysis have different aims](../.gitbook/assets/image%20%2820%29.png)

In summary, both clustering analysis and the trajectory analysis are trying to **organize the sampled cell population based on their molecular similarity**. Only after a meaningful organization, we can then do differential tests or correlation analysis to study specific questions.

### Pseudo-bulk analysis

Once clustering is done, we usually merge cells into pseudo-bulk profiles, so we can perform any analysis just like bulk-seq. The advantage is that the **pseudo-bulk profiles \(juice made from single type of fruit\) are likely coming from more homogeneous cell populations then the tissue bulk profiles are \(juice made from multiple types of fruits\)**.

## Limitations on single-cell technology

### Throughput vs. Coverage

All single-cell sequencing technologies are lowly covered \(at the cell level\) comparing to bulk-seq. However, within the single-cell technologies, the coverage can also be very different. In general, there is a balance between throughput and coverage per cell - high-throughput methods have lower coverage than medium-throughput methods. It is not right to compare technologies only based on their throughput. A fair [comparison](https://www.nature.com/articles/s41587-020-0465-8) needs to consider overall reads utilities, clustering abilities, etc.

### If your cell type of interest is rare

One common problem is that the cell type of interest is relatively rare in the total population. After sequencing, most data come from those major but boring cell types, and little analysis can be done on the rare but interesting cell type. Single cell technology with clustering analysis do help you separate those rare types clearly, but it doesn't help you enrich it. If the data is not covered enough, it is hard to do further analysis after clustering \(e.g., case/ctrl DEG analysis\). [Additional efforts need to be paid before single-cell experiment to optimize your cell population that most suitable for your question](https://www.youtube.com/watch?v=oUFFGVzIgEw). And [serious power analysis](https://www.biorxiv.org/content/10.1101/2020.04.01.019851v1) needs to be considered before doing single-cell experiment.

### Do you really need the single-cell level

Different tissues have different levels of cellular heterogeneity. Single-cell technology can dissect the heterogeneity in the highest resolution, but may not be needed in every situation. For example, if your tissue only contains well-defined cell types \(PBMC again\) and you only care about the difference between cell types rather than within cell types, other simpler technology such as FACS with antibody + bulk-seq already solve the problem. Here are a few situations I think single-cell technology can help:

* The tissue is complex, and the cell type composition is unknown. Such as many regions in the brain.
* The cell-type composition is under dynamic changes in your samples, such as tumor microenvironment. And there is no clear way to separate different cell types \(or too hard to do so due to large heterogeneity\).
* You care about intra-cell-type heterogeneity or continuous change between cell states, such as during development or before/after drug treatment.

## Three questions to summarize single-cell technologies

![Summary of this page](../.gitbook/assets/image%20%283%29.png)

Just like bulk-seq, most single-cell sequencing technologies are not all developed from scratch. When reading a technical paper describing a new single-cell technology, I ask myself three questions: 

* How is the cell isolated? 
* How is the cell barcoded? 
* Which molecular modality/modalities this technology is profiling?

Here I provide the major solutions \(the figure\) that different technologies used to answer the above questions. Single-cell technology can then be described as a combination of their answers. Here are some notable examples:

* 10X Chromium scRNA-seq: This is a high throughput bead-based technology that sequencing single cell 3' mRNA molecule. It introduces cell barcode via the barcoded beads.
* SMART-seq \(RNA\): This is a medium-throughput plate-based technology that sequencing single-cell full-length RNA molecule. It introduces cell barcode via PCR in each well in the plate.
* snmC-seq \(my project\): This is a medium-throughput plate-based technology that profiling single-cell whole-genome DNA methylation. It introduces the cell barcode via PCR in each well in the plate.





![](../.gitbook/assets/_w5a0464.jpeg)

