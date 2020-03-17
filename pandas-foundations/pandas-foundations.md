# pandas Foundations

## Course Description

pandas DataFrames are the most widely used in-memory representation of complex data collections within Python. Whether in finance, a scientific field, or data science, familiarity with pandas is essential. This course teaches you to work with real-world datasets containing both string and numeric data, often structured around time series. You will learn powerful analysis, selection, and visualization techniques in this course.

---

---

## Data ingestion & inspection

[Slides](./01_chapter1.pdf)

### 1. Review of pandas DataFrames

#### Exercise: Inspecting your data

You can use the DataFrame methods `.head()` and `.tail()` to view the first few and last few rows of a DataFrame. In this exercise, we have imported pandas as `pd` and loaded population data from 1960 to 2014 as a DataFrame `df`. This dataset was obtained from the [World Bank](http://databank.worldbank.org/data/reports.aspx?source=2&type=metadata&series=SP.URB.TOTL.IN.ZS#).

Your job is to use `df.head()` and `df.tail()` to verify that the first and last rows match a file on disk. In later exercises, you will see how to extract values from DataFrames with indexing, but for now, manually copy/paste or type values into assignment statements where needed. Select the correct answer for the first and last values in the `'Year'` and `'Total Population'` columns.

##### Instructions

##### Possible Answers

- First: 1980, 26183676.0; Last: 2000, 35.

- First: 1960, 92495902.0; Last: 2014, 15245855.0.

- First: 40.472, 2001; Last: 44.5, 1880.

- First: CSS, 104170.0; Last: USA, 95.203.

<details>
<summary>Solution</summary>

**First: 1960, 92495902.0; Last: 2014, 15245855.0.**

```python
    import pandas as pd
    df = pd.read_csv('datasets/world_ind_pop_data.csv')
    print(df.head())
    print(df.tail())
```

</details>

---

#### Exercise: DataFrame data types

Pandas is aware of the data types in the columns of your DataFrame. It is also aware of null and `NaN` ('Not-a-Number') types which often indicate missing data. In this exercise, we have imported pandas as `pd` and read the world population data into a DataFrame `df` which contains some `NaN` values --- a value often used as a place-holder for missing or otherwise invalid data entries.

Your job is to use `df.info()` to determine information about the total count of `non-null` entries and infer the total count of `null` entries, which likely indicates missing data.

Select the best description of this data set from the following:

##### Instructions

##### Possible Answers

- The data is all of type `float64` and none of it is missing.

- The data is of mixed type, and 9914 of it is missing.

- The data is of mixed type, and 3460 `float64`s are missing.

- The data is all of type `float64`, and 3460 `float64`s are missing.

<details>
<summary>Solution</summary>

**The data is of mixed type, and 3460 `float64`s are missing.**

```python
      import pandas as pd
      df = pd.read_csv('datasets/world_ind_pop_data.csv')
      # df is already manipulated, only original dataset available for download
      df.iloc[0:10380:3, -2] = np.nan
      # Above statement makes dataset similar to one DataCamp gives you on console
      df.info()
```

</details>

---

#### Exercise: NumPy and pandas working together

Pandas depends upon and interoperates with NumPy, the Python library for fast numeric array computations. For example, you can use the DataFrame attribute `.values` to represent a DataFrame `df` as a NumPy array. You can also pass pandas data structures to NumPy methods. In this exercise, we have imported pandas as `pd` and loaded world population data every 10 years since 1960 into the DataFrame `df`. This dataset was derived from the one used in the previous exercise.

Your job is to extract the values and store them in an array using the attribute `.values`. You'll then use those values as input into the NumPy `np.log10()` method to compute the base 10 logarithm of the population values. Finally, you will pass the entire pandas DataFrame into the same NumPy `np.log10()` method and compare the results.

##### Instructions

- Import `numpy` using the standard alias `np`.
- Assign the numerical values in the DataFrame `df` to an array `np_vals` using the attribute `values`.
- Pass `np_vals` into the NumPy method `log10()` and store the results in `np_vals_log10`.
- Pass the entire `df` DataFrame into the NumPy method `log10()` and store the results in `df_log10`.
- Inspect the output of the `print()` code to see the `type()` of the variables that you created.

<details>
<summary>Solution</summary>

```python
    # Import numpy
    import numpy as np
    import pandas as pd

    df = pd.read_csv('datasets/world_population.csv')

    # Create array of DataFrame values: np_vals
    np_vals = df.values

    # Create new array of base 10 logarithm values: np_vals_log10
    np_vals_log10 = np.log10(np_vals)

    # Create array of new DataFrame by passing df to np.log10(): df_log10
    df_log10 = np.log10(df)

    # Print original and new data containers
    [print(x, 'has type', type(eval(x))) for x in ['np_vals', 'np_vals_log10', 'df', 'df_log10']]

```

_Output:_

    np_vals has type <class 'numpy.ndarray'>
    np_vals_log10 has type <class 'numpy.ndarray'>
    df has type <class 'pandas.core.frame.DataFrame'>
    df_log10 has type <class 'pandas.core.frame.DataFrame'>

</details>

---

---

### 2. Building DataFrames from scratch

#### Exercise: Zip lists to build a DataFrame

In this exercise, you're going to make a pandas DataFrame of the top three countries to win gold medals since 1896 by first building a dictionary. `list_keys` contains the column names `'Country'` and `'Total'`. `list_values` contains the full names of each country and the number of gold medals awarded. The values have been taken from [Wikipedia](https://en.wikipedia.org/wiki/All-time_Olympic_Games_medal_table).

Your job is to use these lists to construct a list of tuples, use the list of tuples to construct a dictionary, and then use that dictionary to construct a DataFrame. In doing so, you'll make use of the `list()`, `zip()`, `dict()` and `pd.DataFrame()` functions. Pandas has already been imported as `pd`.

Note: The [`zip()`](https://docs.python.org/3/library/functions.html#zip) function in Python 3 and above returns a special zip object, which is essentially a generator. To convert this `zip` object into a list, you'll need to use `list()`. You can learn more about the `zip()` function as well as generators in [Python Data Science Toolbox (Part 2)](https://www.datacamp.com/courses/python-data-science-toolbox-part-2).

##### Instructions

- Zip the 2 lists `list_keys` and `list_values` together into one list of (key, value) tuples. Be sure to convert the `zip` object into a list, and store the result in `zipped`.
- Inspect the contents of `zipped` using `print()`. This has been done for you.
- Construct a dictionary using `zipped`. Store the result as `data`.
- Construct a DataFrame using the dictionary. Store the result as `df`.

<details>
<summary>Solution</summary>

```python
    import pandas as pd
    list_keys = ['Country', 'Total']
    list_values = [
        ['United States', 'Soviet Union', 'United Kingdom'],
        [1118, 473, 273]
        ]

    zipped = list(zip(list_keys, list_values))  # tuples
    data  = dict(zipped)
    df = pd.DataFrame.from_dict(data)
    print(df)

```

_Output:_

|       | Country        | Total |
| ----- | -------------- | ----- |
| **0** | United States  | 1118  |
| **1** | Soviet Union   | 473   |
| **2** | United Kingdom | 273   |

</details>

---
