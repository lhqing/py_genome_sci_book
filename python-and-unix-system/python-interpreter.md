# 🆕 🎉 Run Python

## Three Ways to Run Python

### 1. Using the default python shell

Most introductory books only tell you one way to run python, which is probably something like this:

```text
$ python
Python 3.7.6 | packaged by conda-forge | (default, Mar 23 2020, 22:45:16)
[Clang 9.0.1 ] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> print('hello world')
hello world

(do something else...)
```

This `python` command starts a **python shell \(it is not like other shells, in the python shell, all you write is python code\)**, which is the default way to start python coding. In the first line, you see it printed out some information about my python installation: `Python 3.7.6 | ...`  

This message is describing my **python interpreter**.

### 2. Using python command to execute a ".py" file

Another way is to use the `python` command to directly execute some python code that's been written in a `.py` script file.

```text
# write the most simple python script
$ echo 'print("hello world")' > hello_world.py

# execute this python script
$ python hello_world.py
hello world
```

The `hello_world.py` can be any python code that's way more complex, but they are all executed by the same **python interpreter** as the one printed out in method 1. You will get the same results if you copy python code one by one into the python shell and execute them in order.

### 3. Using the Jupyter Notebook

The third way \(and **the best way for interactive data analysis**\) to run python is by using the Jupyter Notebook. Just like [this "hello world" example](https://github.com/lhqing/py_genome_sci_book/blob/master/analysis/hello_world/jupyter_hello_world.ipynb).

## **Understand the Python Language**

Definition from Wikipedia: Python is an [interpreted](https://en.wikipedia.org/wiki/Interpreted_language), [high-level](https://en.wikipedia.org/wiki/High-level_programming_language), [general-purpose](https://en.wikipedia.org/wiki/General-purpose_programming_language) [programming language](https://en.wikipedia.org/wiki/Programming_language).

Wordy explanation:

* **Interpreted**: Python script is easy to read by a human, but it can not be recognized by any system kernels. In order to execute ANY python script, there is a "**python interpreter**" that helps you **translate** the python language into some machine language that the system can understand. 
* **High-level**: This means python is relatively easy to understand; many python codes are just like English. Many CS101 courses teach python because it is easy to learn.
* **General-purpose**: This means **python can do anything**, from handling files to dealing with operation system affairs; from generating data tables to make visualizations. You need to find the right way and **package** to do it.

Short version: 

**Python is good for a human, but to run it on an actual machine, you need a python interpreter.**

## Python Interpreter is a "translator" between you and the system.

Python, as a programming language, is just a bunch of **rules** about how to write programs in a standard way. The real implementation of python language rules and what makes it run-able on computers is the **python interpreter**.

When you install python from anaconda or miniconda, you installed a python interpreter called CPython. **The CPython is a program that is written in C programming language to explain the python code you provide to it, and translate it into some complied codes, and run it through the system.** All of the three methods mentioned above eventually bring your python code to the interpreter to run it.

So, an alternative understanding of python language could be that: You are using a C program called CPython \(though one of the three methods above\), this program is so versatile that you even need to learn a whole new language called python to use it. But once you learned python, you can do whatever you want with this program.

This plot explained what happened when you run python:

![https://indianpythonista.wordpress.com/2018/01/04/how-python-runs/](../.gitbook/assets/image%20%2814%29.png)

## API vs CLI vs GUI

Now hopefully, you understand **the three methods to run your python code**. But how about **running other people's code?**

All kinds of packages or programs provide their users with a specific "interface" to use them. There are three main kinds of interfaces: 1. Application Programming Interface \(API\); 2. Command Line Interface \(CLI\); 3. Graphical User Interface \(GUI\).

### API

When you import a python package into the active Jupyter Notebook or your own python script, you are actually using the API of that package. For example

```text
# This is inside your python environment, like a jupyter notebook or python shell

# import a package to start using its API
import pandas as pd

# read a table through function name
pd.read_csv(SOME_TBALE_FILE)
```

The pandas package provides you APIs \(named functions\), so you can use a single line of code to open a file, but no need to worry about how to open that file and how to parse the content.

### CLI

When you execute a command with certain parameters in the shell, you are using a program's CLI. All shell commands like `ls` , `less` have their CLI, so do those bioinformatic tools like `salmon`. The CLI allows a program taking user input from the shell, and performing corresponding react based on it. The programs do not obtain CLI automatically. Indeed, many additional codes need to be written to parse the command line input, and logic needs to be written into the code to give proper responses on all kinds of inputs.

{% hint style="info" %}
Program written by all kinds of programming languages can have CLI. Python program can have it, so does C, Java, or R programs. CLI is just a universal way \(and most common way in UNIX\) to get some input from users and then run the job.
{% endhint %}

Unlike API, not all python packages provide you CLI. Pandas, for example, do not have any CLI; the only way to use it is to import it into python. Because **CLI is only suitable for relatively fixed and straightforward jobs**, for example, map a FASTQ file or print out the content of the current directory. Pandas' capacity is just like Excel, can you imagine including all Excel's functionality into a CLI framework? \(If so, you might have thousands of parameters\) If you can't, you probably understand why we don't need to bother to provide a CLI for pandas.

### GUI

GUI is basically for non-coding people. Since you are reading this book, you don't need it. We \(data scientists or programmers\) don't need it.

## Inside Jupyter Notebook

[See Jupyter Notebook](https://github.com/lhqing/py_genome_sci_book/blob/master/analysis/python_basic/explor_jupyter_notebook_environment.ipynb)

In this notebook, I give you some more details about the method 3 of running python - using the Jupyter Notebook. Once read, you should be able to understand:

* What python interpreter does Jupyter Notebook use?
* How to understand that a running notebook is just a python process with all your variables from each executed cell stored in the background?

## Summary

* There are three ways to run python. They are all needed, but for analysis, use Jupyter Notebook.
* All running python programs rely on the same python interpreter
* You use API all the time when you import a python module/package; Some python package or other software provide you CLI because their job is fixed and straightforward.

