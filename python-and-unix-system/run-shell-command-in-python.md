# 🆕 🎉 Run Shell Command In Python - I

This page is the first part of "run shell command in python", I will introduce you the subprocess package and ways to run command in python. In [the second part](../python-basics-1/run-shell-command-in-python-ii.md), I will introduce some more advanced knowledge about stdin, stdout and pipe with the subprocess package.

## Different ways to run shell command

1. Run a command in the shell
2. Run a command in Jupyter Notebook with "!" or with the magic command "%bash". \(See Jupyter Notebook\)
3. Run a command with python subprocess package

## The subprocess package

When you executed a command, you started a [process](https://www.geeksforgeeks.org/processes-in-linuxunix/) that use specific system resources \(CPU, MEM, etc.\) to run the job. In addition, all process can spawn child processes, which is called subprocess. The python built-in **subprocess package allow you to start subprocess in python**. In other words, it allow you to execute other commands within python, just like what you do in the shell.

## Why run shell command in python?

The main reason is to run batch commands easier.

When I [prepare the bulk RNA-seq data for this book](../get-raw-data/introduction-to-the-datasets/developing-mouse-forebrain-bulk-polya-plus-rna-seq.md), I used the pandas to handle all the metadata table, and use python code to construct dozens of command. Finally, I use the subprocess package to execute them \([see this notebook](https://github.com/lhqing/py_genome_sci_book/blob/master/data/DevFB/3.mapping.ipynb)\). Because everything is done in python, I don't need to switching environments and all steps are documented in the notebook.

## Stdin, stdout, stderr, and return code

You need to understand these terms before reading the subprocess.run\(\) jupyter notebook below.

A UNIX process has three standard streams: stdin, stdout, and stderr.

* stdin is for taking input
* stdout is for printing output informations
* stderr is for printing error informations

These three terms are foundation of UNIX process information flow, I believe you can find great explanations on google if you don't fully understand this.

In addition to the three information stream, all commands finished with a returncode. The UNIX convention is that, if returncode is 0, means command succeed, non-zero returncode means command failed. Different  non-zero returncodes mean different kinds of failure, which is defined by the program.

## subprocess.run\(\)

[See Jupyter Notebook](https://github.com/lhqing/py_genome_sci_book/blob/master/analysis/python_basic/execute_shell_commands_in_python.ipynb)

Take home message of this notebook:

* **subprocess.run\(\)** is the most common API for running shell command in python.
* set **stderr=PIPE** and **stdout=PIPE** to capture the information printed in these two system file handles
* set **encoding='utf8'** to make sure you got string but not bytes from stderr and stdout
* Returncode == 0 means job succeed, otherwise means failure. If **check=True**, non-zero return code triggers **subprocess.CalledProcessError**
* **Try ... Except ...** allows you catch an error and deal with it
* By default, **shell=False** and you need to provide command as a list, redirct and pipe will not work.
* When **shell=True**, you can provide command as a string and any command works just like in shell

{% hint style="success" %}
subprocess.run\(\) is a hard but important python function for beginners, it is not easy to understand, but once you do, you gain a lot of knowledge not only on python, but also on the whole UNIX system!
{% endhint %}











