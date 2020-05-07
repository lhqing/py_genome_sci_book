# Other Tips

## [Oh my zsh](https://github.com/ohmyzsh/ohmyzsh)

Bash is the most common shell, but there are a lot more other options. My favorite shell is zsh, when equip with "Oh my zsh". 

{% embed url="https://github.com/ohmyzsh/ohmyzsh" %}

Give it a try, and you will love it.

### Customize your shell using the config file

Both bash and zsh comes with a config file in your home directory. The one for bash is `~/.bashrc` and the one for zsh is `~/.zshrc`. 

This config file is basically a shell script, execute by the shell when it starts. Usually, I create many alias for common commands such as ssh to a server or start a jupyter notebook, zsh also come with many convenient alias and other [fancy plugins](https://github.com/ohmyzsh/ohmyzsh#plugins) and themes for your shell \(I use `ys` theme\).

## Export your environment for backup and recovering

From this [stack overflow](https://stackoverflow.com/questions/56472295/can-you-export-a-created-python-conda-environment-for-others-to-activate-on-thei) and [export section](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#sharing-an-environment) of conda documentation: 

```text
# enter env first
$ conda activate genome_book
(genome_book)

# export the environment into a yml file, which contains all installation history
$ conda env export --from-history > environment.yml
(genome_book)

# This is the content of that file
$ cat environment.yml
name: genome_book
channels:
  - conda-forge
  - bioconda
  - defaults
dependencies:
  - pandas==1.0.3
  - jupyter==1.0.0
  - scikit-learn==0.22.2.post1
  - pysam==0.15.4
  - seaborn=0.10.0
  - pybedtools==0.8.1
  - python=3.7
  - jupyter_contrib_nbextensions==0.5.1
  - deeptools==3.4.2
prefix: /Users/hq/miniconda3/envs/genome_book
(genome_book)

# recreate the exact environment with the yml file
$ conda env create -f environment.yml
```



