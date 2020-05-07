# Check whether package X is installed

## Method 1: In the shell

If you are using [the environment](../work-environment/chapter-introduction.md) as I introduced, all your third-party python packages are installed under the environment directory. And the python interpreter \(i.e. the `python` command\) already know where they locates, and allow you to import them, just like other built-in python packages.

To check this, just use python interpreter in the shell

```text
# go into the environment

# hq @ Hanqings-iMac in ~ [19:58:58]
$ conda activate genome_book
(genome_book)


# you should see you are using the python interpreter
# from your environment directory

# hq @ Hanqings-iMac in ~ [19:59:14]
$ which python
/Users/hq/miniconda3/envs/genome_book/bin/python
(genome_book)


# Now start the python interpreter

# hq @ Hanqings-iMac in ~ [19:59:21]
$ python
Python 3.7.6 | packaged by conda-forge | (default, Mar 23 2020, 22:45:16)
[Clang 9.0.1 ] on darwin
Type "help", "copyright", "credits" or "license" for more information.


>>> import pandas as pd  # import package X, pd is just a temporary alias for pandas, you can name it whatever you want
>>> pd.__version__  # the above command already confirmed pandas is installed. But this command tell you the exact version
'1.0.3'
```

## Method 2: In Jupyter Notebook

[Here](../work-environment/jupyter-notebook.md#start-jupyter-notebook) I explained how to **start Jupyter Notebook server under the genome\_book environment**.

If you can go into Jupyter, check out [this Jupyter Notebook](https://github.com/lhqing/py_genome_sci_book/blob/master/analysis/hello_world/check_package_installation.ipynb). \(It's in the GitHub Repo as well\)





