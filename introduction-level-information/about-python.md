# About python

## Take An Introductory Course

Here I listed prerequisites for continue reading. Don't be overwhelmed by the long list, because a full understanding of the things below is not required, I will also explain them along the book. In the beginning, you only need to know these names and understand their primary usage and purpose. The best way to do so, is take a well organized course or read a book for beginners. I don't want to repeat their message here, because they just did a much better job than me on this.

Here are my recommendations \(choose any one of them, they are redundant\):

1. Class 1, 2, 3 of this Coursera specialization: [https://www.coursera.org/specializations/python](https://www.coursera.org/specializations/python)
2. Introduction to Python 3 by RealPython: [https://realpython.com/learning-paths/python3-introduction/](https://realpython.com/learning-paths/python3-introduction/)
3. \(If you prefer book, this is my first introduction to python, before Coursera becomes popular. This book also has Chinese version.

   \) Beginning Python: [https://www.amazon.com/Beginning-Python-Professional-Magnus-Hetland-ebook/dp/B06XGVVVMG](https://www.amazon.com/Beginning-Python-Professional-Magnus-Hetland-ebook/dp/B06XGVVVMG). 

It might take several days to finish the introduction contents, but it helps you build up a reliable knowledge graph for future study.

## The Python Language

* Basic data types: int, float, str
* Basic data structure: list, dict, set
* Control flow: if, for, break, continue, try...except...
* [Python built-in functions](https://docs.python.org/3/library/functions.html): range\(\), any\(\), all\(\), enumerate\(\), dir\(\), help\(\), isinstance\(\), open\(\), print\(\) and others.
* Python built-in modules \(just knowing what they are and the general usage, google and youtube can be helpful\): 
  * system and file related: pathlib, subprocess, json, gzip, multiprocessing, concurrent.futures
  * [Regular Expressions](https://regexone.com/): re
  * Other enhancement on control flow or data structure: collections, random, itertools

{% hint style="info" %}
[Python built-in modules](https://docs.python.org/3/library/index.html): The built-in modules come with python installation, and can be considered part of python language. Python is a versatile language for almost all programming application, so does its built-in modules. Not all modules are necessary for daily genome science.
{% endhint %}

## Third-Party Packages

* [Numpy](https://numpy.org/): The "N-dimensional array" data structure in python, everything related to linear algebra based on this. In other words, everything based on this.
* [Pandas](https://pandas.pydata.org/docs/getting_started/index.html): The "Excel" in python, handle your tables. Must learn for genome science.
* [scipy](https://www.scipy.org/), [scikit-learn](https://scikit-learn.org/stable/), and [statsmodels](https://www.statsmodels.org/stable/index.html): The statistics and basic machine learning packages for Python \(and many other applications out of my knowledge\). They all contain tons of functions, but here are simple examples on each:
  * scipy: some basic statistical tests \(t, Wilcoxon, fisher\_exact\), build dendrogram, sparse matrix format.
  * scikit-learn: PCA, Kmeans, RandomForest, and many other models/algorithms
  * statsmodels: build linear models, multi-test correction, ANOVA
* [matplotlib](https://matplotlib.org/), and [seaborn](https://seaborn.pydata.org/): The must-learn python visualization package. For publication purpose, these two are enough for any figure, your imagination is the limit.

{% hint style="info" %}
Other third-party packages: Packages listed here are the primary packages for data science, but there are many others for more specific applications. With them, you can achieve most of the purpose in several lines of code. If you feel like some purpose needs more than 100 lines of code to succeed, you are likely reinventing the wheels. Try search google and see if someone already achieved that for you in a beautiful package \(happens so many times on me\). 
{% endhint %}

{% hint style="info" %}
Some great learning materials for introduction:

* [10 minutes to pandas](https://pandas.pydata.org/pandas-docs/stable/getting_started/10min.html): explain pandas usage in ~~10 mins~~ maybe an hour... 
* [The python ecosystem for Data Science](https://www.youtube.com/watch?v=EBgUiuFXE3E): This youtube video explains all packages listed here.
* [Seaborn tutorial](https://seaborn.pydata.org/tutorial.html): The Seaborn documentation is a beautiful tutorial not only for the package, but also for the data visualization principles.
{% endhint %}

