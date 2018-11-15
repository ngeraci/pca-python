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

Today we'll be working through an example with metadata from the [Jay Kay Klein collection](https://calisphere.org/collections/26943/) of science fiction convention photographs. We'll use the [pandas](http://pandas.pydata.org/) data analysis library in Python to rename, reorder, add, split, edit, and delete columns.


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
                                                 Title                        .
..                                                                     People
0          Richard Lupoff, Argosy distribution, Pittcon                        .
..                                                  Lupoff, Richard A., 1935-
1          Richard Lupoff, Argosy distribution, Pittcon                        .
..                                                  Lupoff, Richard A., 1935-
2                                  Party scene, Pittcon                        .
..                              De Camp, L. Sprague (Lyon Sprague), 1907-2000
3                        Cutting into the cake, Pittcon                        .
..                                                             Dinkleman, Ann
4                                  Party scene, Pittcon                        .
..                                                             Dinkleman, Ann
5                                  Party scene, Pittcon                        .
..                                                             Dinkleman, Ann
6             Isaac Asimov and fans conversing, Pittcon                        .
..                                                   Asimov, Isaac, 1920-1992
7           Forrest J Ackerman in conversation, Pittcon                        .
..                                                       Ackerman, Forrest J.
8                  Bjo Trimble at dealers room, Pittcon                        .
..                                                               Trimble, Bjo
9                        Avram Davidson at bar, Pittcon                        .
..                                                            Davidson, Avram
10                Ed Emshwiller, prominent fan, Pittcon                        .
..                                                             Emshwiller, Ed
...                                                 ...                        .
..                                                                        ...

1636  John Schoenherr, "The Role of the Artist in Sc...                        .
..                                                           Schoenherr, John
1637  Jack Gaughan, "The Role of the Artist in Scien...                        .
..                                                              Gaughan, Jack
1638                         Families in bar, Noreascon                        .
..                                                           Bova, Ben, 1932-
1639         Larry Niven speaking at closing, Noreascon                        .
..                                                               Niven, Larry
1640         Larry Niven speaking at closing, Noreascon                        .
..                                                               Niven, Larry
1641  Tony Lewis and Charlie Brown long shot of clos...                        .
..                          Lewis, Tony;Brown, Charles N. (Charles Nikki),...
1642  Jack Chalker and Joe Mayhew speaking at art au...                        .
..                                    Chalker, Jack L.;Mayhew, Joe, 1942-2000

[1643 rows x 5 columns]
~~~
{: .output}

We can see that there were 1643 rows parsed. Each row has 5
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
of all of the column names in our data frame. We can also view specific columns by selecting them like this:
`klein_df["Title"]`.

> ## Try out the methods below to see what they return.
>
> 1. `klein_df.columns`
> 2. `klein_df.head()` - Also, what does `klein_df.head(15)` do?
> 3. `klein_df.tail()`
{: .challenge}
