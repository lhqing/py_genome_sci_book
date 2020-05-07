# bulk RNA-seq

This book aims to explain coding skills related to data cleaning and visualization, and I choose the dataset to represent typical data structure. You don't need to worry whether the biology question or the species fits your project, because the programming skills have great universality.

The first dataset I will use in this book is a bulk RNA-seq dataset. This dataset is [downloaded from the ENCODE project](https://www.encodeproject.org/search/?type=Experiment&status=released&assay_slims=Transcription&lab.title=Barbara+Wold%2C+Caltech&biosample_ontology.term_name=forebrain&assay_title=polyA+plus+RNA-seq), containing 16 bulk polyA-plus RNA-seq experiments. All data comes from a more massive project profiling many other tissues in the same way, but for simplicity, I will only use the forebrain tissue as an example.

{% hint style="success" %}
I provided all my code for preprocessing this dataset from downloading FASTQ to salmon quant result. All steps were done with python + shell command in the Jupyter Notebook. I want to emphasize two good practices of doing analysis:

1. Everything can be documented within the Jupyter notebook to allow good reproducibility.
2. I create a metadata table for each step to give each set of files meaningful annotations instead of relying on a super long file name that contains everything.

Packages used in the preprocessing steps:

* Jupyter notebook: record all your python code, markdown notes, and shell command in the same notebook, together with all the results and visualization. 
* Python packages I used: 
  * subprocess: run any shell command from python 
  * pathlib: handle path related stuff 
  * pandas: the "excel" in python.
* Other RNA-seq softwares:
  * Trim Galore: FASTQ QC and trimming, based on another two packages called fastqc and cutadapt
  * salmon: For mapping and quantify RNA reads
{% endhint %}

## Experiment Design

The samples are forebrain tissues from eight time points during mouse embryo development. Each time point has two biological replicates.

| Development Time Point | Replicate 1 | Replicate 2 |
| :--- | :--- | :--- |
| E10.5 | - | - |
| E11.5 | - | - |
| E12.5 | - | - |
| E13.5 | - | - |
| E14.5 | - | - |
| E15.5 | - | - |
| E16.5 | - | - |
| P0 | - | - |

{% hint style="info" %}
E10.5 means embryo day 10.5; P0 means postnatal day 0. See [this page](https://embryology.med.unsw.edu.au/embryology/index.php/Mouse_Timeline_Detailed) to get a bit more knowledge about mouse embryo development.
{% endhint %}

I choose this dataset because:

* It has good data quality, and all time points have two replicates.
* We can do simple differential analysis between two timepoints, to mimic case-control like study.
* We can also do time-series analysis, taking advantage of the ordered developmental timepoints.

## The preprocessing steps

I provide whole preprocessing steps to allow you to get a sense of how this is done using python and shell script to do preprocessing and using Jupyter notebook to document everything. The actual computation is done on a server, which you don't need to repeat. I've provided the processed raw data \(raw salmon results\) [on github](developing-mouse-forebrain-bulk-polya-plus-rna-seq.md#get-this-dataset) for all further steps, which are doable on most laptops.

{% hint style="info" %}
Some quick notes before you read the Jupyter notebooks

1. Jupyter notebook supports markdown so that I can write my explanations in a rich format easily.
2. When a cell contains lines start with "!", it will be interpreted as a shell command, executed via your system default shell, providing a convenient way to put python and shell script together.
3. Other cells are all python code and output.
4. [A beginner's guide on Jupyter Notebook](https://towardsdatascience.com/a-beginners-tutorial-to-jupyter-notebooks-1b2f8705888a)
{% endhint %}

{% hint style="info" %}
The python code in Jupyter notebook is not fully explained, but provided as records of how I did the work. I will recap many of them and explain in the following chapters.
{% endhint %}

### Step 1. Download data, rename the files and make a metadata table

[See Jupyter notebook](https://nbviewer.jupyter.org/github/lhqing/py_genome_sci_book/blob/master/data/DevFB/1.DownloadAndPrepareMetadata.ipynb)

In this notebook, I did the following steps:

1. Download all the FASTQ files from ENCODE.
2. Prepare a metadata table, contains all necessary sample information for each downloaded file.
3. Rename the files with meaningful names \(the original names are meaningless ids for computer\).

### Step 2. FASTQ QC

[See Jupyter notebook](https://nbviewer.jupyter.org/github/lhqing/py_genome_sci_book/blob/master/data/DevFB/2.fastqTrimAndQC.ipynb)

In this notebook, I did the following steps:

1. I did FASTQ trimming and QC using [trim\_galore](https://www.bioinformatics.babraham.ac.uk/projects/trim_galore/) on each FASTQ file from step 1. I also write a parallel computation example using the python built-in `concurrent.futures` package to fasten computation. 
2. The FASTQ file information comes from the metadata table from step 1. I also made another metadata table for the trimmed FASTQ. 

### Step 3. Salmon Mapping

[See Jupyter notebook](https://nbviewer.jupyter.org/github/lhqing/py_genome_sci_book/blob/master/data/DevFB/3.mapping.ipynb)

In this notebook, I did the following steps:

1. I did salmon quant on each sample. There are 16 samples but 25 trimmed FASTQ files. All samples were single-end sequenced, so they all mapped using single-end mode. Some samples have 2 FASTQ files, and they need to be provided to `salmon quant` together. [In the code](https://nbviewer.jupyter.org/github/lhqing/py_genome_sci_book/blob/master/data/DevFB/3.mapping.ipynb#Prepare-salmon-command-for-each-sample), I explained how this could be easily done with python \(and the pandas.Dataframe\)
2. The trimmed FASTQ file information comes from the metadata table from step 2. I also made another metadata table for the salmon output. 

### The Raw Processed Data

After mapping, I provide you the raw processed data to start the analysis, including:

1. 16 `salmon quant` raw outputs for each RNA-seq sample
2. A metadata table that contains experiment design information
3. The original GTF file \(GENCODE mouse vm24\) used to build the salmon index. I will play with it more in the following pandas chapters.

## Get this dataset

All files are included in the [Github repository](https://github.com/lhqing/py_genome_sci_book) of this book. 

```text
# if you haven't got the github repo
git clone https://github.com/lhqing/py_genome_sci_book.git
# if you already did, git pull will update it
git pull

cd py_genome_sci_book/data/DevFB
# where the data and notebook locates

cd py_genome_sci_book/ref/GENCODEvM24
# where the gene annotation gtf locates
```

{% hint style="info" %}
FASTQ files and the salmon index are not included in github, because they are too large and not needed for further analysis.
{% endhint %}

