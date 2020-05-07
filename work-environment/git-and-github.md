# Git and Github

{% hint style="info" %}
Git and Github are fundamental tools for CS, which I don't think I've fully explored. Yet, the primary usage of git and Github is still essential for my work, so here I only give you some basic introductions based on what I know and may add much more stuff in the future if I learn more about them.
{% endhint %}

{% hint style="info" %}
Minimum things you should know are:

* Github is the host I used to save and share with you the code and small data files.
* it's based on git.
* Use git and Github for each one of your project.
{% endhint %}

## Git

From git [home page](https://git-scm.com/):

> Git is a free and open-source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

Git helps you:

1. manage the history of ALL your files related to a certain package \(usually inside a single directory, which is called a repository\). It adds the "save" and "rollback" bottom to your whole directory.
2. Together with Github, it backups your files online in a remote repository.
3. It allows multiple people to collaborate together. Indeed, most packages hosted on Github has dozens or even hundreds of contributors.

## Github

While git controls your local file, Github is the remote host that allows you to upload your local repository into a Github repository. It's free! 

{% hint style="info" %}
Github repo is not intended for hosting large files \(&gt; 100 MB\). It's usually used for hosting code, text documentation \(markdown\), Jupyter notebook file, some small dataset. If you save large raw data in the same directory, you can use `.gitignore` file to exclude them from backing up to Github. Use other ways \(google drive, etc.\) to back up large files.
{% endhint %}

## Use git and Github

I do not want to explain git in detail, because there are tons of material introducing git and Github for beginners. Here are my suggestions to start:

* Check your terminal, whether `git` is installed.
* Create a [Github account](https://github.com/join?source=header-home). \(This is [mine](https://github.com/lhqing)\)
* Watch this [3min video from Github](https://www.youtube.com/watch?v=w3jLJU7DT5E).
* Read this neat introduction: [https://rogerdudler.github.io/git-guide/](https://rogerdudler.github.io/git-guide/)
* Once you understand basic git command \(`git clone`, `add`, `commit`, `push`, `checkout`, `merge`\), you can use [Github Desktop - GUI from Github](https://desktop.github.com/) for easier controlling.
* Clone or fork \(in Github, fork means make a duplication of this repo to your Github\) [my Github repo for this book](https://github.com/lhqing/py_genome_sci_book).

{% hint style="info" %}
[Learn a bit more about git ignore](https://help.github.com/en/github/using-git/ignoring-files) to prevent adding large file or temp file into your git repo.
{% endhint %}

{% hint style="info" %}
My Github repo is still updating until this tip disappears. If you cloned my repo, use`git pull`to update it.
{% endhint %}

## Clone Github Repository of This Book

To get all the data and jupyter notebooks for this book:

```text
$ cd /To/The/Place/You/Want/To/Save/This/Repo/

$ git clone https://github.com/lhqing/py_genome_sci_book.git

$ cd py_genome_sci_book/data/
# This is the data directory

$ cd ../analysis/
# This is the analysis diretroy, will contain .ipynb files

# If you want to update this repository from github, go back to the repo dir
$ cd /To/The/Place/You/Want/To/Save/This/Repo/py_genome_sci_book

$ git pull
```

{% hint style="info" %}
I do not recommend direct changing this repository directory, because you may encounter some git errors when you are trying the `git pull` , if that happened and you can't solve it, delete this directory and rerun `git clone`. But that means all your custom changes will be gone.
{% endhint %}

