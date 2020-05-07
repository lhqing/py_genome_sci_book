# Chapter Ensemble

In this chapter, I will discuss all setups for the work environment before starting analysis.

**This page contains quick steps for creating same work environment in 5 mins.** 

The following pages will explain details: 

1. [All About Installations](conda-and-pip.md): How to install python, python packages, and other bioinformatic programs related to this book.
2. [Keep Running](let-it-run.md): How to keep your command running in the shell.
3. [Coding Environment](jupyter-notebook.md): Using Jupyter Notebook/Lab for data analysis, and useful tips to enhance efficiency.
4. [Git and Github](git-and-github.md): Using Git and Github while you do coding and analysis.
5. [Other tips](oh-my-zsh.md): Some other optional tips.

## Step 1. Installation

### 1.1 Install minicoda or anaconda

Install any one of them from here: [miniconda](https://docs.conda.io/en/latest/miniconda.html) or [anaconda](https://www.anaconda.com/distribution/)

### 1.2 Setup python environment and packages for this book

```bash
# setup conda channels
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge

# remove the incomplete environment if you did
conda env remove -n genome_book

# create the environment and install everything in one command!
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
```

### 1.3 Use screen to start jupyter notebook

```bash
# this creates a new screen named jupyter
screen -R jupyter
```

```bash
# In the new screen

# go back to your home direcotry
cd ~
# jupyter can only read file from the directory it starts, 
# if you run the jupyter in a subdirectory, 
# it can not reach other files on your computer.

# enter the env
conda activate genome_book

# optionally, setup your jupyter password
jupyter notebook password

# start jupyter notebook
jupyter notebook

# jupyter will keep running in the screen even if you cloase the terminal
# You should see the jupyter URL from its stdout
```

### 1.4 In jupyter notebook extension tab, select your favorite extensions

![These are my selections](../.gitbook/assets/image%20%2812%29.png)

### 1.5 clone the repository from github

```text
$ cd /To/The/Place/You/Want/To/Save/This/Repo/

$ git clone https://github.com/lhqing/py_genome_sci_book.git
```

Now in jupyter notebook navigator, go to the github repo, you can start browse my code and data.

![](../.gitbook/assets/image%20%2825%29.png)

![file in py\_genome\_sci\_book/analysis/hello\_world/jupyter\_hello\_world.ipynb](../.gitbook/assets/image%20%282%29.png)



Now everything is installed!



![](../.gitbook/assets/img_0246.jpeg)

