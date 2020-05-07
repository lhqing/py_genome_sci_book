---
description: Let's start with CORRECT installation
---

# All About Installations

{% hint style="info" %}
If you just want to quickly create the same environment as I will use in this book, read the code snippet in the end.
{% endhint %}

Installation is usually a pain-in-the-ass step. It is especially frustrated for beginners when being stopped at the first step of the analysis after spending a long time finishing an introduction course; I was one of them. So on this page, I want to detail explain how I install and manage my packages.

## What does installation mean?

{% hint style="info" %}
If this paragraph is hard to understand, read the following sections first and then go back to read this summary. 
{% endhint %}

In python, installation means you use an [**installation command**](conda-and-pip.md#installation-command) to install [**specific package**](conda-and-pip.md#specific-packages)\(s\) from a [**package repository**](conda-and-pip.md#package-repository) into a [**package environment**](conda-and-pip.md#package-environment). The default and other named [**package environments**](conda-and-pip.md#package-environment) were controlled by the [**package manager**](conda-and-pip.md#package-manager).

## Python 3, not P~~ython 2~~

**ONLY USE PYTHON 3.** If you are just new to python, don't bother to understand what is python2. It's an old version that's been deprecated by the python world now.

## Package manager

[Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/getting-started.html) is the most wildly used package manager for python. You can install conda in two ways:

1. Install with the [miniconda](https://docs.conda.io/en/latest/miniconda.html). A minimal installation of conda
2. Install with the [anaconda](https://www.anaconda.com/distribution/). Comprehensive installation of conda and many basic data-science packages.
3. I prefer miniconda cause its small. But anaconda also works fine.

```bash
# after install either miniconda or anaconda, 
# in your terminal, check if conda correctly installed:
$ conda -V
```

### More about conda

`conda` manages not only python package, but also other packages/softwares writing in R or any other programming languages. Conda contains multiple subcommands, the most used ones are:

* `conda install` install packages
* `conda create` create conda environments
* `conda env` handle conda environments
* `conda config` set up things like conda channel

## Installation command

there are two shell commands for installing packages:

* `pip install PACKAGE_NAME`: pip is the default installer comes with python
* `conda install PACKAGE_NAME`: A more sophisticated installer comes with conda.
* How to choose these two?
  * **When the package is installable via conda, choose conda over pip.** Because conda checks the package **dependency graph** more thoroughly, which means less pain.
  * However, many immature/developing package \(e.g., a new package from a paper\) only provide pip install options, then use pip.

{% hint style="info" %}
**Dependency Graph**: when you install a python package, the installer actually installs dozens of other packages. Because most packages in python are NOT built from scratch, it `import` many other packages for existing functionalities. Their dependencies are described in a [dependency graph](https://www.google.com/search?q=dependency+graph+python&rlz=1C5CHFA_enUS764US765&sxsrf=ALeKk01CUkqjDaRs4aEh5WUBeXZ1C-pk5Q:1586452272175&source=lnms&tbm=isch&sa=X&ved=2ahUKEwj8h4uh69voAhXLPn0KHdcjAq0Q_AUoAXoECA8QAw&biw=2500&bih=1306&dpr=2), and the installer needs to phrase the graph to install all necessary packages.
{% endhint %}

## **Specific packages**

The word "specific" means both the **name** and the **version** of a package. Because different versions of the same package can be incompatible. It is good to install a specific version. For example, when you install a package called `pandas`, command 1 is better than 2 for production:

```bash
# command 1:
conda install pandas=1.X.X  
# the "=1.X.X" means the version, 
# should be specific number depending on the available pandas version

# command 2: 
conda install pandas  # this, by default, install the newest version available
```

How to determine which version to install? 

* If no specific conflicts, install the newest stable version, you may use command 2 first, but in the end, I gave you the exact version number I used for this book.

## Package repository

Python also has two package repositories, one for pip, one for conda:

* [PyPI](https://pypi.org/): this is where `pip` download package file when you execute `pip install PACKAGE_NAME`
* [conda](https://anaconda.org/): yes, the word `conda` has multiple meanings... But basically, this is where conda download package file `conda install PACKAGE_NAME`, importantly, conda has different channels hosting different packages. You should set it up first \(see below\).  

### Conda [Channels](https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/channels.html#id1)

Conda has multiple channels, which serve as the base for hosting and managing different packages. Conda has a default channel, but there are two other important channels for genome science:

* **conda-forge**: where many important analysis packages are
* **bioconda**: most bioinformatic packages installed from here.

### [Bioconda](https://bioconda.github.io/)

Bioconda is a channel for the conda package manager specializing in bioinformatics software. It **not only host python packages but also host the most common bioinformatic softwares**: bwa, bowtie, samtools, bedtools, vcftools, deeptools, STAR, salmon, cutadapt, so on so forth.

Almost everything is installable via conda.

### How to set up your conda channels?

```bash
# In your terminal, execute these commands in the same order:
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge

# this means when you run "conda install", 
# conda first check conda-forge, then bioconda, then defaults
```

## Package environment

### My Practice

A [conda environment](https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/environments.html) is a **directory** that contains a specific collection of conda packages that you have installed.

In my practice, **I create separate conda environments for each of my projects.** The environment isolates everything I installed for one project from the other, so they don't intermingle and give me great consistency.

If you don't do that, every time you install a new package, it will be installed into the default environment, and a new version will overwrite old one, which might contain incompatible changes that break your existing code.

### How to create an environment?

Let's check the default python used currently, the `which` command tells you where an executable command file actually located.

```bash
$ which python
/Users/hq/miniconda3/bin/python

# I use miniconda, and the default python is in the miniconda3 dir
```

Now we create an environment called "genome\_book" for this book and use the python 3.7. Then we enter this environment, check out python location again.

```bash
$ conda create -n genome_book python=3.7
(skip the long stdout text)

$ conda activate genome_book
# I entered the env now

$ which python
/Users/hq/miniconda3/envs/genome_book/bin/python
# The python location changed! 
# Everything will refer to the environment's version of python


# Let's go to look at the environment directory
$ cd /Users/hq/miniconda3/envs/genome_book/

$ ls -hl
total 0
drwxr-xr-x  109 hq  staff   3.4K Apr  9 11:06 bin
drwxr-xr-x   21 hq  staff   672B Apr  9 11:06 conda-meta
drwxr-xr-x  112 hq  staff   3.5K Apr  9 11:06 include
drwxr-xr-x   92 hq  staff   2.9K Apr  9 11:06 lib
drwxr-xr-x    3 hq  staff    96B Apr  9 11:06 man
drwxr-xr-x    8 hq  staff   256B Apr  9 11:04 share
drwxr-xr-x    9 hq  staff   288B Apr  9 11:04 ssl
# you can see the environment is just an standalone direcotry 
# that contains everything.
```

Next, let's install an example package into this environment. You will see **tools installed inside an environment, are only available when you enter this environment**. In this way, the environment isolates things!

```bash
# installation
$ conda install -n genome_book bedtools
(skip the long stdout text)
# IMPORTANT: the -n genome_book means only install the bedtools into this env


# make sure you still inside your environment, 
# if not, run the above conda activate again
$ which bedtools
/Users/hq/miniconda3/envs/genome_book/bin/bedtools
# bedtools installed!

# now let's go out of this environment
$ conda deactivate
# I am out of the environment now

$ which bedtools
bedtools not found
# bedtools not found!

$ which python
/Users/hq/miniconda3/bin/python
# python location also change back to my conda default
```

### If you are curious, how does the environment change work?

Here is how the above magic works; the key is the[ "PATH" environmental variable](http://www.linfo.org/path_env_var.html). 

The PATH variable is a list of directory paths, where the shell uses to find a command's actual location. It is separated by the ":" character. Directory appears first, will be searched first, and once found, the searching will stop. By changing the PATH variable, the conda environment controls your command priority. 

```bash
$ conda deactivate
# make sure you are out of the environment

$ echo $PATH
/Users/hq/miniconda3/condabin:/Users/hq/bin:/usr/local/bin:/Users/hq/lib/hadoop-3.0.0/bin:/Users/hq/lib/spark-2.2.1-bin-hadoop2.7/bin:/Users/hq/lib/scala-2.12.4/bin:/usr/local/mysql/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Applications/Server.app/Contents/ServerRoot/usr/bin:/Applications/Server.app/Contents/ServerRoot/usr/sbin
# My default PATH variable
# You can see the "/Users/hq/miniconda3/condabin" is the first path.
# This means the shell will first search in my miniconda defalut directory


# we then go into the env, check PATH again
$ conda activate genome_book
# I entered the env now

$ echo $PATH
/Users/hq/miniconda3/envs/genome_book/bin:/Users/hq/miniconda3/condabin:/Users/hq/bin:/usr/local/bin:/Users/hq/lib/hadoop-3.0.0/bin:/Users/hq/lib/spark-2.2.1-bin-hadoop2.7/bin:/Users/hq/lib/scala-2.12.4/bin:/usr/local/mysql/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Applications/Server.app/Contents/ServerRoot/usr/bin:/Applications/Server.app/Contents/ServerRoot/usr/sbin
# Now the env dir "/Users/hq/miniconda3/envs/genome_book/bin" is the first path. 
# Shell will search the env dir first!
```

**The environment is a great idea; we should all use it!**

## Summary: creating the environment for this book

This page is a very wordy introduction to the installation... But I do waste tons of time on installing things before I understand the above knowledge. Here is a summary code snippet to entirely create a same environment as I will use in this book:

```bash
# Make sure you install either miniconda or anaconda

# First, setup conda channels
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge

# Second, remove the incomplete environment created above if you did
conda env remove -n genome_book

# Third, create the environment and install everything in one command!
# These packages will be used in this book
conda create -n genome_book \
    python=3.7 \
    pandas==1.0.3 \
    seaborn=0.10.0 \
    jupyter==1.0.0 \
    jupyter_contrib_nbextensions==0.5.1 \
    scikit-learn==0.22.2.post1 \
    pysam==0.15.4 \
    deeptools==3.4.2 \
    pybedtools==0.8.1 \
    scanpy=1.4

# Forth, enter the env
conda activate genome_book

# Fifth, check python
which python

# All done!
```



Consistency 🍻!



![](../.gitbook/assets/image%20%2810%29.png)

