# Coding Environment

## Python Environments

There are multiple ways to code and run python. Some people may only use a text editor and the original python interpreter; some may use the IDEs; for data-analysis-oriented coding, I highly suggest using the Jupyter notebook.

### Python interpreter

```text
$ python
Python 3.7.6 | packaged by conda-forge | (default, Mar 23 2020, 22:45:16)
[Clang 9.0.1 ] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> print("hello world!")
hello world!
```

This is the basic python interpreter. I do not use this directly for production, but it is used by all other environments bellow, they make this basic interpreter more convenient to use. I will explain what a python interpreter is in [another page](../python-and-unix-system/python-interpreter.md).

### [ipython kernel](https://ipython.readthedocs.io/en/stable/index.html)

`ipython` kernel **built on top of the python interpreter**, providing a more convenient way to run python. It is the default python kernel used by Jupyter notebook. I do not use it directly via shell. I use it with its high-level GUI, the Jupyter Notebook.

### Jupyter notebook or lab

Jupyter notebook is my only working environment for daily analysis. Here are the main reasons I like it: 

* Like a lab notebook, it integrates all your code and annotation, and figures in one file. Everything is self-explanatory.
* It executes not only python code, but also shell commands. Using different  [kernels](https://jupyter.readthedocs.io/en/latest/projects/kernels.html), it can also execute many other languages like R or even [run python and R in a same notebook](https://stackoverflow.com/questions/39008069/r-and-python-in-one-jupyter-notebook). For python, the ipython kernel is used.
* Abundant [notebook extensions](jupyter-notebook.md#notebook-extensions) make my life much easier.

[Jupyter Lab](https://jupyterlab.readthedocs.io/en/stable/) is another kind of GUI form Jupyter, which is termed as "next-generation", check that out if you like, but I haven't fully switched to that in 2020, maybe I will, when it's more mature.

{% hint style="info" %}
For analysis, I use Jupyter notebook, Jupyter notebook uses ipython kernel, ipython kernel uses the python interpreter.
{% endhint %}

### IDE

IDE is a more comprehensive developing environment. I use [PyCharm](https://www.jetbrains.com/pycharm/) when I develop python packages for the basic infrastructure of my project. But I do not use it for daily analysis or this book. When you are getting more familiar with programming and starting to build your tools, you will need to know more about [PyCharm](https://www.jetbrains.com/pycharm/).

{% hint style="info" %}
For package development, I use PyCharm, PyCharm uses the python interpreter.
{% endhint %}

## Start Jupyter Notebook

Jupyter Notebook has a web server, you start and keep the server process on running, and use it through a web browser:

```text
# remember to go into your environment that installed jupyter notebook and all other packages
$ conda activate genome_book
(genome_book)

# Start jupyter is just one command:
$ jupyter notebook
[I 17:44:42.958 NotebookApp] [jupyter_nbextensions_configurator] enabled 0.4.1
[I 17:44:44.049 NotebookApp] JupyterLab extension loaded from /Users/hq/miniconda3/envs/genome_book/lib/python3.7/site-packages/jupyterlab
[I 17:44:44.049 NotebookApp] JupyterLab application directory is /Users/hq/miniconda3/envs/genome_book/share/jupyter/lab
[I 17:44:44.060 NotebookApp] Serving notebooks from local directory: /Users/hq/Documents/pkg/py_genome_sci_book/analysis/hello_world
[I 17:44:44.060 NotebookApp] The Jupyter Notebook is running at:
[I 17:44:44.060 NotebookApp] http://localhost:8888/?token=3bf94daea7b735bb796af59ea4a31e9c8061b47632600af8
[I 17:44:44.060 NotebookApp]  or http://127.0.0.1:8888/?token=3bf94daea7b735bb796af59ea4a31e9c8061b47632600af8
[I 17:44:44.061 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 17:44:44.067 NotebookApp]

    To access the notebook, open this file in a browser:
        file:///Users/hq/Library/Jupyter/runtime/nbserver-19557-open.html
    Or copy and paste one of these URLs:
        http://localhost:8888/?token=3bf94daea7b735bb796af59ea4a31e9c8061b47632600af8
     or http://127.0.0.1:8888/?token=3bf94daea7b735bb796af59ea4a31e9c8061b47632600af8
```

By default, [http://localhost:8888/](http://localhost:8888/) is the URL to open your jupyter notebook navigator. The token is just a temporary password. Setting up a real password for jupyter is more convenient, it's explained [here](https://jupyter-notebook.readthedocs.io/en/stable/public_server.html#automatic-password-setup):

```text
$ jupyter notebook password
Enter password:  ****
Verify password: ****
[NotebookPasswordApp] Wrote hashed password to /Users/you/.jupyter/jupyter_notebook_config.json
```

{% hint style="info" %}
I suggest you [use a named screen](let-it-run.md#screen) for jupyter command because it needs to be always alive when doing your analysis.
{% endhint %}

### ipynb file

Here is a simple example of [jupyter notebook](https://nbviewer.jupyter.org/github/lhqing/py_genome_sci_book/blob/master/analysis/hello_world/jupyter_hello_world.ipynb). When you save it from jupyter notebook page, it becomes a `.ipynb` file, which is a special [JSON format](https://en.wikipedia.org/wiki/JSON) that contains all your code, markdown notes, and other metadata.

It can be viewed in:

* The jupyter notebook webserver
* [nbviewer](https://nbviewer.jupyter.org/), a website rendering any notebooks from public github repositories.
* [nteract](https://nteract.io/applications), a GUI app for jupyter

## Notebook extensions

Jupyter notebook comes with rich third-party extensions that make it highly efficient, [in the installation step](conda-and-pip.md#summary-creating-the-environment-for-this-book), I added the `jupyter_contrib_nbextensions` package, which is a collection of most jupyter notebook extensions. Because it's installed, you can see an additional panel called `Nbextensions` in your jupyter navigator. You can activate any extensions from here. Not all of them are useful, but here are the ones I used:

![](../.gitbook/assets/image%20%2812%29.png)

Spend a few minutes to read those ones come with documentation and customize your jupyter notebook environment!

## [Papermill](https://papermill.readthedocs.io/en/latest/)

Often times, after finishing an analysis in a jupyter notebook, we want to **rerun it with different input files or test different parameters**. Copy notebook files and changing all the value is tedious and error-prone. Here is a great tool that solves this problem! With simple modifications, it turns any notebook into a parameterized pipeline:

* Step 1: write a notebook template [with a parameter cell](https://papermill.readthedocs.io/en/latest/usage-parameterize.html#designate-parameters-for-a-cell)
* Step 2: write an [execution notebook](https://papermill.readthedocs.io/en/latest/usage-execute.html#execute-via-the-python-api) or use the [command line interface](https://papermill.readthedocs.io/en/latest/usage-execute.html#execute-via-cli) to automatically execute the template notebook with different parameters! 

{% hint style="info" %}
Papermill is not very good at taking complex input \(such as a dict with special object in it\), better use simple data type \(number, string, simple list etc.\) in the parameter cells, if you really have complex needs, I usually solve that in two ways:

* Write additional logic determine complex input from simple parameter in another cell
* Use more sophisticated config file such as an `.ini` or `.yaml` and only provide their path as a parameter to papermill. I hardly find this is necessary.
{% endhint %}

