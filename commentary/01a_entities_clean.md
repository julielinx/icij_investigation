---
output:
  word_document: default
  html_document: default
---


```python
import numpy as np
import pandas as pd

pd.options.display.max_rows = 999
pd.options.display.max_columns = 999
pd.options.display.max_colwidth = 150
```

<font color='orangered'>**Hinata**</font>: Hey, Kageyama, what's that stuff in the first box?

<font color='midnightblue'>**Kageyama**</font>: The 'box' is called a cell. Didn't you look at the [Jupyterlab Docs](https://jupyterlab.readthedocs.io/en/stable/user/notebook.html) or [Jupyter Notebook Tutorial](https://www.dataquest.io/blog/jupyter-notebook-tutorial/) Suga recommended?

<font color='goldenrod'>**Tsukishima**</font>: The Tutorial is very basic. Even you should be able to follow it.

<font color='orangered'>**Hinata**</font>: Hey!!

<font color='midnightblue'>**Kageyama**</font>: If you can't sit still long enough for those, here's [a video](https://www.youtube.com/watch?v=K2Yb1nXTmYM) that's less than five minutes.

<font color='goldenrod'>**Tsukishima**</font>: You're overestimating his intelligence and reasoning skills. Here's a [two hour video on Jupyterlab basics](https://www.youtube.com/watch?v=Gzun8PpyBCo). Maybe you'll come away from that a little smarter.

<font color='gray'>**Sugawara**</font>: Don't forget, Tsukishima. Not everyone has the computer science background you do.

<font color='goldenrod'>**Tsukishima**</font>: ~*Tsk*~

<font color='gray'>**Sugawara**</font>: Kageyama, why don't you explain the code you put in the first cell.

<font color='midnightblue'>**Kageyama**</font>: It's two libraries and some pandas display settings.

<font color='orangered'>**Hinata**</font>: What're libraries?

<font color='midnightblue'>**Kageyama**</font>: Learn to code, dumbass! Haven't you finished the [University of Michigan Python 3 Programming Specialization](https://www.coursera.org/specializations/python-3-programming?) I showed you??

<font color='orangered'>**Hinata**</font>: It's a set of five courses and each one takes like 20 hours! It's gonna take *forever*!!!

<font color='hotpink'>**Yachi**</font>: Those courses are in English. Shouldn't we give him ones in Japanese?

<font color='midnightblue'>**Kageyama**</font>: If he's gonna be needy, he can find his own courses.

<font color='goldenrod'>**Tsukishima**</font>: If he ever does manage to finish it, he can say he took a course from a US university. I'm sure his resume could use all the padding it can get.

<font color='orangered'>**Hinata**</font>: C'mon guys, what's a library?

<font color='goldenrod'>**Tsukishima**</font>: ~*Tsk*~

<font color='goldenrod'>**Tsukishima**</font>: A place with a lot of books.

<font color='midnightblue'>**Kageyama**</font>: ~*Glare*~

<font color='midnightblue'>**Kageyama**</font>: Libraries are fundamental to high level computer languages.

<font color='hotpink'>**Yachi**</font>: A **high level computer language** is one that's easier for *people* to read and write.

<font color='hotpink'>**Yachi**</font>: Computers understand things in 1s and 0s. Languages closer to what *computers* understand are called **low level computer languages** and are generally really hard for people. Examples include assembly or machine code.

<font color='hotpink'>**Yachi**</font>: Because they're easier for people to work with, there are a lot more high level languages. Some of them are Python, R, Ruby, Julia, and Java.

<font color='midnightblue'>**Kageyama**</font>: Right. Yeah. What she said.

<font color='midnightblue'>**Kageyama**</font>: So, a library is written in a specific language and is basically a collection of code that's already written for you.

<font color='green'>**Yamaguchi**</font>: Loading every library for a given language would use up a lot of your computer's memory, so you only load the ones you need. Each library has a group of related functions for specific kinds of tasks.

<font color='orangered'>**Hinata**</font>: ~*Oooohhh!*~

<font color='orangered'>**Hinata**</font>: What about the display settings? What's the 999 stuff about?

<font color='green'>**Yamaguchi**</font>: By default pandas only shows **60 rows and 20 columns**. Kageyama got the biggest dataset, so probably he probably upped the number of rows and columns so he could see more data at once.

<font color='orangered'>**Hinata**</font>: Oh. Okay!

## Load data


```python
keep_cols = ['node_id', 'sourceID', 'name', 'incorporation_date', 'country_codes', 'countries',
             'jurisdiction_description', 'jurisdiction', 'service_provider', 'status']
dtypes = {'node_id': 'int32', 'sourceID':'category', 'name':'object', 'country_codes':'category', 'countries':'category',
          'jurisdiction_description':'category', 'jurisdiction':'category', 'service_provider':'category', 'status':'category'}

bahamas_entity_raw = pd.read_csv('../data/raw/bahamas_leaks/bahamas_leaks.nodes.entity.csv', 
                                 usecols = keep_cols,
                                 dtype=dtypes)
offshore_entity_raw = pd.read_csv('../data/raw/offshore_leaks/offshore_leaks.nodes.entity.csv', 
                                 usecols = keep_cols,
                                 dtype=dtypes)
panama_entity_raw = pd.read_csv('../data/raw/panama_papers/panama_papers.nodes.entity.csv', 
                                 usecols = keep_cols,
                                 dtype=dtypes)
paradise_entity_raw = pd.read_csv('../data/raw/paradise_papers/paradise_papers.nodes.entity.csv', 
                                 usecols = keep_cols,
                                 dtype=dtypes)
```

<font color='orangered'>**Hinata**</font>: Wait! Wait! What're 'keep_cols' and 'dtypes'? And why'd you put them in the read_csv function after the file path??

<font color='goldenrod'>**Tsukishima**</font>: We're never going to get through this notebook.

<font color='midnightblue'>**Kageyama**</font>: 'keep_cols' is a list variable representing the columns we want to keep from the original data. The CSVs had a bunch of empty or extraneous columns.

<font color='midnightblue'>**Kageyama**</font>: 'dtypes' is a dictionary variable that specifies the data types to use for each column. I figured out which data type takes up the least amount of memory for each column.

<font color='hotpink'>**Yachi**</font>: Using less memory to store data allows that memory to be used to process data. It helps keep processing speeds faster when working with the large datasets.

<font color='orangered'>**Hinata**</font>: How'd you know which columns to keep and what data type to use?

<font color='midnightblue'>**Kageyama**</font>: It's obvious when you look at the data.

<font color='orangered'>**Hinata**</font>: Kaaageeeeyaaaamaaaa...

<font color='midnightblue'>**Kageyama**</font>: Load the data and look at it yourself, scrub! You obviously need the practice.

<font color='green'>**Yamaguchi**</font>: Suga-senpai asked us to show how we got our solutions and explain our reasoning so we could learn from each other.

<font color='midnightblue'>**Kageyama**</font>: It's faster my way.

<font color='goldenrod'>**Tsukishima**</font>: You failed every class where the teacher required you to show your work, didn't you?

<font color='midnightblue'>**Kageyama**</font>: Shut up! 

<font color='midnightblue'>**Kageyama**</font>: And stop messing up my notebook. If you guys are going to ask dumbass questions, do it somewhere else.

(See 01b_entities_kageyamaanswersdumbassquestions.ipynb for an explaination on how Kageyama came up with the code below.)

## Standardize column order and concatenate dataframes


```python
bahamas_entity_raw = bahamas_entity_raw[keep_cols]
offshore_entity_raw = offshore_entity_raw[keep_cols]
panama_entity_raw = panama_entity_raw[keep_cols]
paradise_entity_raw = paradise_entity_raw[keep_cols]

entity_df = pd.concat([bahamas_entity_raw, offshore_entity_raw, panama_entity_raw, paradise_entity_raw], ignore_index=True)
```

## Standardize formatting

- Null entries imported as a string 'nan' instead of an actual null value.
- Capitalization is all over the place. Standardized as title case.


```python
entity_df.replace('nan', np.nan, inplace=True)
entity_df['name'] = entity_df['name'].str.title()
```

## Consolidate entries in 'status' column


```python
entity_df['status'] = entity_df['status'].str.lower()
entity_df.loc[entity_df['status'].str.contains('liquidation', na=False), 'status'] = 'in liquidation'
entity_df.loc[entity_df['status'].str.contains('liquidated', na=False), 'status'] = 'liquidated'
entity_df.loc[entity_df['status'].str.contains('resigned', na=False), 'status'] = 'resigned agent'
entity_df.loc[entity_df['status'].str.contains('sundry', na=False), 'status'] = 'sundry account'
entity_df.loc[entity_df['status'].str.contains('dissolved', na=False), 'status'] = 'dissolved'
entity_df.loc[entity_df['status'].str.contains('struck|defunct|deregistered', na=False), 'status'] = 'struck / defunct / deregistered'   
entity_df['status'] = entity_df['status'].str.title()
```

## Format date


```python
entity_df.loc[
    (entity_df['incorporation_date'].str.contains('[A-Z]{3}', na=False)) & ((entity_df['incorporation_date'].str[-4:] > '2018') | (entity_df['incorporation_date'].str[-4:] < '1800')
                                                                           ), 'incorporation_date'] = np.nan
entity_df['formatted_date'] = pd.to_datetime(entity_df.loc[entity_df['incorporation_date'].str.contains(',', na=False), 'incorporation_date'], format='%b %d, %Y')
entity_df['formatted_date'] = pd.to_datetime(entity_df.loc[entity_df['incorporation_date'].str.contains('[A-Z]{3}', na=False), 'incorporation_date'], format='%d-%b-%Y')

entity_df.drop(columns=['incorporation_date'], inplace=True)
entity_df.rename(columns={'formatted_date':'incorporation_date'}, inplace=True)
```

## Address duplicates and worthless entries

- 'counry_codes' and 'countries' are strings that are actually lists. Not standardized as to which value comes first in the list, causing duplicates when counting values.
- 'jurisdiction' and 'jurisdiction_description' included worthless values that should be null


```python
entity_df['country_codes'] = entity_df.loc[entity_df['country_codes'].notnull(), 'country_codes'].str.split(';').apply(lambda x: sorted(x))
entity_df['countries'] = entity_df.loc[entity_df['countries'].notnull(), 'countries'].str.split(';').apply(lambda x: sorted(x))
entity_df['jurisdiction_description'] = entity_df['jurisdiction_description'].str.title()
entity_df.loc[entity_df['jurisdiction_description'].str.contains('Undetermined|Recorded in leaked files as "fund"'), 'jurisdiction_description'] = np.nan
entity_df['jurisdiction'] = entity_df['jurisdiction']
entity_df.loc[entity_df['jurisdiction'] == 'XXX', 'jurisdiction'] = np.nan
```


```python
entity_df.head(3)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>node_id</th>
      <th>sourceID</th>
      <th>name</th>
      <th>country_codes</th>
      <th>countries</th>
      <th>jurisdiction_description</th>
      <th>jurisdiction</th>
      <th>service_provider</th>
      <th>status</th>
      <th>incorporation_date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20003127</td>
      <td>Bahamas Leaks</td>
      <td>Dalma Corporation Limited</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bahamas</td>
      <td>BAH</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1990-11-30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20010494</td>
      <td>Bahamas Leaks</td>
      <td>Asia Construction Corporation Limited</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bahamas</td>
      <td>BAH</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1992-08-14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20010495</td>
      <td>Bahamas Leaks</td>
      <td>Euro Logistics Limited</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bahamas</td>
      <td>BAH</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1992-08-14</td>
    </tr>
  </tbody>
</table>
</div>



<font color='midnightblue'>**Kageyama**</font>: At the team's insistance, we're also removing 'Not identified' and 'XXX' from the 'countries' and 'country_code' columns.

<font color='goldenrod'>**Tsukishima**</font>: And made you put in this disclaimer so you wouldn't 'accidentally' take credit for it, Your Majesty.

<font color='midnightblue'>**Kageyama**</font>: Don't call me that!!

<font color='goldenrod'>**Tsukishima**</font>: Yes, Your Highness. Anything you say, Sire.

<font color='midnightblue'>**Kageyama**</font>: !!!!


```python
def clean_country_and_code(df):
    df['country_codes'].replace('XXX', np.nan, inplace=True)
    df['country_codes'].str.replace(';XXX|XXX;', '')
    df['country_codes'] = df.loc[df['country_codes'].notnull(), 'country_codes'].str.split(';').apply(lambda x: sorted(x))
    df['countries'].replace('Not identified', np.nan, inplace=True)
    df['countries'].str.replace(';Not identified|Not identified;', '')
    df['countries'] = df.loc[df['countries'].notnull(), 'countries'].str.split(';').apply(lambda x: sorted(x))
    
clean_country_and_code(entity_df)
```


```python
entity_df.to_csv('../data/intermediate/entities.csv')
```
