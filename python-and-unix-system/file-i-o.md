---
description: 'Read/write your data table, or any python object from/to files'
---

# 🆕 🎉 File I/O

All data analysis start from reading files into memory and end with saving results into new files. Here I summarized everything you need to know about files, and how to read and write files in python. For those genome science specific file formats, I will talk about how to deal with them in a separate chapter \("GENOME SCIENCE DATA"\)

## Text file & binary file

### What is the difference?

Text files is human-readable, while binary files are for programs. 

For example, a SAM file \(basic genomic file format that contains reads and alignment information\) is a text file. You can directly read it with `less`; a BAM file is a binary version of SAM file, you can not get the same information using `cat` or `less` , you need special software called `samtools` to parse it back into SAM format.

### Their Relationship

Text files can be **encoded** into binary files, while binary files can be **decoded** using certain **standards** into text files.

If you took any computer programming introduction course, you must hear of the **ASCII standard.** It is the most common standard to turn a character into a number, which is called **encoding**. And the number can be converted back into character using the same standard, which is called **decoding**.

Similarly, another widely used encoding standard in python world is called **`utf8`** , you don't need to understand its details, but you will see this name a lot when you need to [**convert bytes \(contents read from binary source\) into string \(human readable\)**](https://stackoverflow.com/questions/606191/convert-bytes-to-a-string).

### Are binary file formats all the same?

No, they are not. Binary files are files contain a lot of numbers. But when we define a binary file format, we can **assign specific positions with special meaning**. For example, we can use the first 100 numbers to save some metadata information \(usually called a **header**\), and the real content starts from the 101 number. In this case, the first 100 numbers need to be skipped when decoding the content, otherwise, they will become meaningless characters after decoding. 

[BAM format](https://samtools.github.io/hts-specs/SAMv1.pdf), for example, contains a header part, which is used for many metadata storage \(e.g., how and when this file is generated, using what genome assembly\). When you use `samtools` to read a bam file, it knows how to correctly parse or skip the header, while if you directly parse the data from the beginning using python, things will all mess up.

## File Compression

You can compress both text or binary files to reduce their sizes, but the compression will not change their file type. BTW, a compressed file is usually a binary file, but many programs will recognize it and decompress it automatically to get the correct content. Like `salmon quant` command can take the gzipped FASTQ file directly because it decompresses the file into FASTQ internally during mapping.

Also, the BAM file is much smaller than SAM file because it's special binary encoding and compression. But when you use `samtools` to view the BAM files, all the decoding and decompression happens inside `samtools` automatically.

## Python basic file I/O

[See Jupyter Notebook](https://nbviewer.jupyter.org/github/lhqing/py_genome_sci_book/blob/master/analysis/file_io/basic_python_io.ipynb)

I suggest you try those code by yourself. Once done, you should be able to explain:

* Read/Write text or binary files
* Read/Write gzipped files
* string and bytes
* encode and decode
* File handle and the cursor location
* Read line by line, read lines, read certain position

## Pandas file I/O

[See Jupyter Notebook](https://github.com/lhqing/py_genome_sci_book/blob/master/analysis/file_io/pandas_io.ipynb)

Pandas is the excel for python. It can handle all the tabular data, super flexible and highly efficient - if using it in the right way.

More details about the pandas dataframe will be covered in a [later page](../data-cleaning/pandas-basics.md).

After reading the notebook, you should be able to explain:

* Read/Write CSV/TSV files, compressed or uncompressed
* Use HDF to speed up large files' I/O

{% hint style="info" %}
[HDF5 format](https://en.wikipedia.org/wiki/Hierarchical_Data_Format) is a special data format that's designed to store large and heterogeneous data. It's a widely used data format in single-cell sequencing. The main reason to use it is its fast I/O speed. **For a large data table \(GBs\), using HDF5 can be 10 times faster than using csv.gz or tsv.gz**
{% endhint %}

## Serialization of Python Objects

[See Jupyter Notebook](https://github.com/lhqing/py_genome_sci_book/blob/master/analysis/file_io/serialization_any_object.ipynb)

Not only your data, but most of the python objects can actually be serialized onto disk. This is realized by some special packages. There are several packages to choose:

* pickle: python built-in package for serializing objects
* joblib: serialization package from sklearn
* json: serialize python dict

**For simplicity, I suggest using joblib.**

{% hint style="info" %}
Using `joblib`, you can serialize any python built-in data structure, a pre-trained machine learning model, or most complex python objects. Load them back into memory is also just one line of code. But serialization is not designed for really large data \(GBs of data\), but it is OK for most processed data or data containing objects.
{% endhint %}

