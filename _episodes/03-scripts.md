---
title: "Scripts"
teaching: ??
exercises: ??
questions:
- "How do you save Python code in a file and run it from the shell?""
---

# Scripts

In the previous section, we walked through manipulating our metadata in the interactive Python interpreter. However, in practice, it's often more efficient to save your Python code as a script, and run it from a file.

Here are all the commands from the previous section:

```
# import pandas library
import pandas as pd

# load data from csv file
klein_df = pd.read_csv("ms381.csv")

# add new columns with known values
klein_df['Creator'] = 'Klein, Jay Kay'
klein_df['Type'] = 'image'
klein_df['Form/Genre 1'] = 'photographic negative'

# rename columns
newcols = {'ARK': 'Identifier', 
    	   'Date': 'Date 1',
    	   'Local Identifier': 'Local Identifier 1'}
klein_df.rename(columns=newcols, inplace=True)

# split 'People' column by semicolon
people = pd.DataFrame(klein_df['People'].str.split(';').tolist())
people.columns = ['Subject (Name) ' + str(col + 1) for col in people.columns]

# re-join "People" dataframe to main klein_df
klein_df = klein_df.join(people)

# set column order
klein_df = klein_df[['Identifier', 'Title', 'Local Identifier 1', 'Date 1',
       				 'Subject (Name) 1', 'Subject (Name) 2', 'Subject (Name) 3',
       				 'Subject (Name) 4', 'Subject (Name) 5']]

# write new csv file called 'pandas_test_export.csv'
klein_df.to_csv('pandas_test_export.csv', index=False)
```
{: .source}

In your plain-text editor, open a new blank file. Copy and paste the above, and save the file with the name "pandas_test.py". Python files should generally end with the file extension `.py`.

You'll notice I've also added some lines, starting with a pound sign, that contain explanatory comments. In Python, starting a line with a pound sign means it's a comment, and you can write notes there that aren't executed as part of the code. Commenting your code is considered good practice, and can be especially helpful in remembering what you're doing as you're learning.

Now let's make a couple of minor changes to the code. First, in our last line, let's change the name of our new CSV file to 'pandas_script_test_export.csv'. Second, let's add one more line at the end of the file:

~~~
print('All done. Awesome work!'')
~~~
{: .source}

The contents of your file, "pandas_test.py", should now look like this:
~~~
# import pandas library
import pandas as pd

# load data from csv file
klein_df = pd.read_csv('ms381.csv')

# add new columns with known values
klein_df['Creator'] = 'Klein, Jay Kay'
klein_df['Type'] = 'image'
klein_df['Form/Genre 1'] = 'photographic negative'

# rename columns
newcols = {'ARK': 'Identifier', 
    	   'Date': 'Date 1',
    	   'Local Identifier': 'Local Identifier 1'}
klein_df.rename(columns=newcols, inplace=True)

# split 'People' column by semicolon
people = pd.DataFrame(klein_df['People'].str.split(';').tolist())
people.columns = ['Subject (Name) ' + str(col + 1) for col in people.columns]

# re-join "People" dataframe to main klein_df
klein_df = klein_df.join(people)

# set column order
klein_df = klein_df[['Identifier', 'Title', 'Local Identifier 1', 'Date 1',
       				 'Subject (Name) 1', 'Subject (Name) 2', 'Subject (Name) 3',
       				 'Subject (Name) 4', 'Subject (Name) 5']]

# write new csv file called 'pandas_script_test_export.csv'
klein_df.to_csv('pandas_script_test_export.csv', index=False)

print('All done! Awesome work.')
~~~
{: .source}

Now, let's run this script from the shell:

~~~
python pandas_test.py
~~~
{: .source}

You should see some familiar friendly output on your screen:

~~~
All done! Awesome work.
~~~
{: .output}

And if you check your working directory, you should see an additional file called 'pandas_script_test_export.csv'

