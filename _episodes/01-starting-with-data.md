---
title: "Starting With Data"
teaching: ??
exercises: ??
questions:
- "How does Python deal with data tables?"
objectives:
- "Explain what a library is, and what libraries are used for."
- "Load a Python/Pandas library."
- "Read tabular data from a file into Python using Pandas using *read_csv*."
- "Learn about the Pandas data frame object."

keypoints:
- "Core concepts in python: Python libraries, Pandas data frames, working with data."

# training: http://swcarpentry.github.io/instructor-training
training: do-we-have-a-repo-of-python-training-resources ?
---

# Working with data in Python

Python is considered a general-purpose programming language. People use it for lots of different things: there are specialized libraries for image processing, for analyzing scientific data, for web development, and pretty much anything you can think of. But one way it can be especially useful in archives and digital library work is for tidying and transforming metadata or other data that's stored in tabular (spreadsheet-style) formats.

Today we'll be working through an example with metadata from the [Jay Kay Klein collection](https://calisphere.org/collections/26943/) of science fiction convention photographs. We'll use the [pandas](http://pandas.pydata.org/) data analysis library in Python to rename, reorder, add, edit, and delete columns.


## About (software) libraries

A library in Python contains a set of tools (called functions) that perform
tasks on our data. As mentioned above, there are many different libraries that exist to help accomplish different tasks. Importing a library is a bit like setting up a piece of specialized equipment.
Once a library is set up, it can be used or called to perform many tasks.


Python doesn't load all of the libraries available to it by default. We have to
add an `import` statement to our code in order to use the library.

So let's start by importing pandas:
~~~
import pandas as pd
~~~
{: .source}

We use the syntax `import [library] as [abbreviation]` so that we won't have to type the whole library name every time we want to use one of its functions.


# Reading CSV data using Pandas

Our data is in CSV format (comma-separated values). So our next step will be to load it using the pandas `read_csv` function. We're going to load it into a data frame, which is a spreadsheet-like data structure used in pandas.

~~~
pd.read_csv("ms381.csv")
~~~
{: .source}

The above command gives us the output below:

~~~
	 URL        											...			Place
0    https://calisphere.org/item/ark:/86086/n2gx48qv        ...         Pittsburgh (Pa.)
1    https://calisphere.org/item/ark:/86086/n2c53j0v        ...         Pittsburgh (Pa.)
2    https://calisphere.org/item/ark:/86086/n27d2s84        ...         Pittsburgh (Pa.)
3    https://calisphere.org/item/ark:/86086/n23n21js        ...         Pittsburgh (Pa.)
4    https://calisphere.org/item/ark:/86086/n2000073        ...         Pittsburgh (Pa.)
5    https://calisphere.org/item/ark:/86086/n2v69grv        ...         Pittsburgh (Pa.)
6    https://calisphere.org/item/ark:/86086/n2qf8r1j        ...         Pittsburgh (Pa.)
7    https://calisphere.org/item/ark:/86086/n2fx77kg        ...         Pittsburgh (Pa.)
8    https://calisphere.org/item/ark:/86086/n2b56gv2        ...         Pittsburgh (Pa.)
9    https://calisphere.org/item/ark:/86086/n26d5r4r        ...         Pittsburgh (Pa.)
10   https://calisphere.org/item/ark:/86086/n2kp8096        ...         Pittsburgh (Pa.)

..   ...        											...			...

189  https://calisphere.org/item/ark:/86086/n2tb153n        ...         Pittsburgh (Pa.)
190  https://calisphere.org/item/ark:/86086/n2pk0dbg        ...         Pittsburgh (Pa.)
191  https://calisphere.org/item/ark:/86086/n2js9nm6        ...         Pittsburgh (Pa.)
192  https://calisphere.org/item/ark:/86086/n2f18wws        ...         Pittsburgh (Pa.)
193  https://calisphere.org/item/ark:/86086/n298855v        ...         Pittsburgh (Pa.)
194  https://calisphere.org/item/ark:/86086/n25h7df4        ...         Pittsburgh (Pa.)
195  https://calisphere.org/item/ark:/86086/n21v5c44        ...         Pittsburgh (Pa.)
196  https://calisphere.org/item/ark:/86086/n2x34vnr        ...         Pittsburgh (Pa.)
197  https://calisphere.org/item/ark:/86086/n2sb43xd        ...         Pittsburgh (Pa.)
198  https://calisphere.org/item/ark:/86086/n2nk3c63        ...         Pittsburgh (Pa.)

[199 rows x 10 columns]

~~~
{: .output}

We can see that there were 199 rows parsed. Each row has 10
columns. It looks like  the `read_csv` function in pandas read our file properly. However,
we haven't saved any data to memory so we can work with it. We need to assign the
data frame to a variable. We can create a new  object with a variable name by assigning a value to it using `=`.

Let's call the data `klein_df`:

~~~
klein_df = pd.read_csv("ms381.csv")
~~~
{: .source}

Notice when you assign the imported data frame to a variable, Python does not
produce any output on the screen. We can print the value of the `klein_df`
object by typing its name into the Python command prompt.

~~~
klein_df
~~~
{: .source}

which prints contents like above.

### Useful ways to view data frame objects in Python

There are multiple methods that can be used to summarize and access the data
stored in data frames. Let's try out a few. Note that we call the method by using
the object name *klein_df.method*. So `klein_df.columns` provides an index
of all of the column names in our data frame.

> ## Try out the methods below to see what they return.
>
> 1. `klein_df.columns`
> 2. `klein_df.head()` - Also, what does `klein_df.head(15)` do?
> 3. `klein_df.tail()`
{: .challenge}
