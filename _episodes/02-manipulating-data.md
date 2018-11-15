---
title: "Manipulating data"
teaching: ??
exercises: ??
questions:
- "How can we use Python and pandas to make bulk edits to metadata?"
---

# Manipulating data

Now that we've loaded and viewed our data, we're going to use pandas to make changes to it and save a new version of it.

## Add new columns with known values
There are a few pieces of information that are consistent across this collection, but aren't currently recorded in the metadata. For example, for every item, we want the "Creator" field to be "Klein, Jay Kay", "Type" to be "image", and "Form/Genre 1" to be "photographic negative." Let's add these fields.

~~~
klein_df['Creator'] = 'Klein, Jay Kay'
klein_df['Type'] = 'image'
klein_df['Form/Genre 1'] = 'photographic negative'
~~~
{: .source}

## Rename columns
Perhaps we're migrating this data to a new digital asset management system that uses different field names, so we also want to change names of some of the columns. First, we'll create a dictionary, where we can match old names (left) to new names (right). Then we'll use a pandas function to rename the columns with those names.

~~~
newcols = {'ARK': 'Identifier', 
    	   'Date': 'Date 1',
    	   'Local Identifier': 'Local Identifier 1'}

klein_df.rename(columns=newcols, inplace=True)
~~~
{: .source}

## Split a column into multiple columns using a delimiter
Our "People" column looks like it sometimes contains more than one name, separated by semicolons, like `Heinlein, Robert A. (Robert Anson), 1907-1988;Smith, E. E. (Edward Elmer), 1890-1965`. We want to split this column into multiple columns, with one name per column, and we want them to be titled "Subject (Name) 1," "Subject (Name) 2," and so forth.

We're going to do this by creating a new dataframe for the People names, and then splitting the values on the semicolon character. 
~~~
people = pd.DataFrame(klein_df['People'].str.split(';').tolist())
~~~
{: .source}

Then we're going to give the columns sequential names that begin with "Subject (Name)":
~~~
people.columns = ['Subject (Name) ' + str(col + 1) for col in people.columns]
~~~
{: .source}

## Join two data frames
Since we made a separate data frame for our personal names, we now need to join that back to our main `klein_df` dataframe.

~~~
klein_df = klein_df.join(people)
~~~
{: .source}


## Set column order
We want to make sure the columns are output in a specific order.

Let's first take a look at what columns we have now:

~~~
klein_df.columns
~~~
{: .source}

~~~
Index(['Title', 'Identifier', 'Local Identifier 1', 'Date 1', 'People',
       'Subject (Name) 1', 'Subject (Name) 2', 'Subject (Name) 3',
       'Subject (Name) 4', 'Subject (Name) 5'],
      dtype='object')
~~~
{: .output}

This looks pretty good, but in our new system, we need to have the Identifier field in the first column for the metadata to ingest properly. And oops, we still have our old, combined 'People' field, which we don't want. Here's what we'll do:

~~~
klein_df = klein_df[['Identifier', 'Title', 'Local Identifier 1', 'Date 1',
       				 'Subject (Name) 1', 'Subject (Name) 2', 'Subject (Name) 3',
       				 'Subject (Name) 4', 'Subject (Name) 5']]
~~~
{: .source}

We've moved the Identifier field to the first column, and left off the People field.

## Representing blank values
We also want to make sure that fields that are missing values are just represented as blanks (''), not with "None" or "0" or other similar values. Here's how we do that:

~~~
klein_df = klein_df.fillna('')
~~~
{: .source}

## Export to a new CSV file
Finally, we want to export our changed data to a new CSV file.

~~~
klein_df.to_csv('pandas_test_export.csv', index=False)
~~~
{: .source}

(We use "index=False" here because otherwise, pandas' default is to add an additional column with row numbers, and we don't generally want that in our metadata)

Awesome! We now have a brand new spreadsheet, saved to the file "pandas_test_export.csv"