# pandas Foundations

## Course Description

pandas DataFrames are the most widely used in-memory representation of complex data collections within Python. Whether in finance, a scientific field, or data science, familiarity with pandas is essential. This course teaches you to work with real-world datasets containing both string and numeric data, often structured around time series. You will learn powerful analysis, selection, and visualization techniques in this course.

### 1. Data ingestion & inspection
[Slides](./01_chapter1.pdf)


#### Exercise: Inspecting your data

You can use the DataFrame methods `.head()` and `.tail()` to view the first few and last few rows of a DataFrame. In this exercise, we have imported pandas as `pd` and loaded population data from 1960 to 2014 as a DataFrame `df`. This dataset was obtained from the [World Bank](http://databank.worldbank.org/data/reports.aspx?source=2&type=metadata&series=SP.URB.TOTL.IN.ZS#).

Your job is to use `df.head()` and `df.tail()` to verify that the first and last rows match a file on disk. In later exercises, you will see how to extract values from DataFrames with indexing, but for now, manually copy/paste or type values into assignment statements where needed. Select the correct answer for the first and last values in the `'Year'` and `'Total Population'` columns.

##### Instructions

##### Possible Answers

-   First: 1980, 26183676.0; Last: 2000, 35.

-   First: 1960, 92495902.0; Last: 2014, 15245855.0.

-   First: 40.472, 2001; Last: 44.5, 1880.

-   First: CSS, 104170.0; Last: USA, 95.203.

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

#### Exercise: DataFrame data types

Pandas is aware of the data types in the columns of your DataFrame. It is also aware of null and `NaN` ('Not-a-Number') types which often indicate missing data. In this exercise, we have imported pandas as `pd` and read the world population data into a DataFrame `df` which contains some `NaN` values --- a value often used as a place-holder for missing or otherwise invalid data entries.

Your job is to use `df.info()` to determine information about the total count of `non-null` entries and infer the total count of `null` entries, which likely indicates missing data.

Select the best description of this data set from the following:

##### Instructions


##### Possible Answers

-   The data is all of type `float64` and none of it is missing.

-   The data is of mixed type, and 9914 of it is missing.

-   The data is of mixed type, and 3460 `float64`s are missing.

-   The data is all of type `float64`, and 3460 `float64`s are missing.

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
