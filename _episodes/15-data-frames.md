---
title: "Pandas DataFrames"
teaching: 15
exercises: 15
questions:
- "How can I do statistical analysis of tabular data?"
objectives:
- "Select individual values from a Pandas dataframe."
- "Select entire rows or entire columns from a dataframe."
- "Select a subset of both rows and columns from a dataframe in a single operation."
- "Select a subset of a dataframe by a single Boolean criterion."
keypoints:
- "Use `DataFrame.loc[..., ...]` and `DataFrame.iloc[..., ...]` to select values by location (name or index, respectively)."
- "Use `:` on its own to mean all columns or all rows."
- "Result of slicing can be used in further operations."
- "Use comparisons to select data based on value."
- "Select values or NaN using a Boolean mask."
---

## Use `DataFrame.loc[columns, rows]` to select values by location using column and row names.

*   Note that `.loc` is followed by square brackets `[]`, not parentheses `()`.

~~~
data = pandas.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
print(data.loc["Albania", "gdpPercap_1952"])
~~~
{: .python}
~~~
1601.056136
~~~
{: .output}

*   Use the `:` notation to slice columns and/or rows (just like lists)

~~~
print(data.loc["Albania":"Germany", "gdpPercap_1952"])
~~~
{: .python}
~~~
country
Albania                   1601.056136
Austria                   6137.076492
Belgium                   8343.105127
Bosnia and Herzegovina     973.533195
Bulgaria                  2444.286648
Croatia                   3119.236520
Czech Republic            6876.140250
Denmark                   9692.385245
Finland                   6424.519071
France                    7029.809327
Germany                   7144.114393
Name: gdpPercap_1952, dtype: float64
~~~
{: .output}

~~~
print(data.loc["Albania":"Belgium", "gdpPercap_1952":"gdpPercap_1967"])
~~~
{: .python}
~~~
         gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  gdpPercap_1967
country
Albania     1601.056136     1942.284244     2312.888958     2760.196931
Austria     6137.076492     8842.598030    10750.721110    12834.602400
Belgium     8343.105127     9714.960623    10991.206760    13149.041190
~~~
{: .output}


## Use `DataFrame.iloc[columns, rows]` to select values by numerical indices.

~~~
print(data.iloc[15:20, 2:5])
~~~
{: .python}
~~~
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy           8243.582340    10022.401310    12269.273780
Montenegro      4649.593785     5907.850937     7778.414017
Netherlands    12790.849560    15363.251360    18794.745670
Norway         13450.401510    16361.876470    18965.055510
Poland          5338.752143     6557.152776     8006.506993
~~~
{: .output}

Note that the second index is NOT inclusive when using `.iloc`. So
`[1:3]` will only return values at index 1 and 2 (typical python
behavior). However, when using `.loc`, **the slicing is inclusive at
both ends**.

## Two ways to access specific columns directly, without `.loc`

*   Pass in a column name as a string between square brackets `[]`

~~~
print(data["gdpPercap_1952"])
~~~
{: .python}
~~~
country
Albania                    1601.056136
Austria                    6137.076492
Belgium                    8343.105127
Bosnia and Herzegovina      973.533195
...
Spain                      3834.034742
Sweden                     8527.844662
Switzerland               14734.232750
Turkey                     1969.100980
United Kingdom             9979.508487
Name: gdpPercap_1952, dtype: float64
~~~
{: .output}

*   To retrieve multiple columns in this way, provide the names in a list

~~~
print(data[["gdpPercap_1952", "gdpPercap_1972"]])
~~~
{: .python}
~~~
                        gdpPercap_1952  gdpPercap_1972
country
Albania                    1601.056136     3313.422188
Austria                    6137.076492    16661.625600
Belgium                    8343.105127    16672.143560
Bosnia and Herzegovina      973.533195     2860.169750
...
Spain                      3834.034742    10638.751310
Sweden                     8527.844662    17832.024640
Switzerland               14734.232750    27195.113040
Turkey                     1969.100980     3450.696380
United Kingdom             9979.508487    15895.116410
~~~
{: .output}

*   Attach the column name directy with a `.`

~~~
print(data.gdpPercap_1952)
~~~
{: .python}
~~~
country
Albania                    1601.056136
Austria                    6137.076492
Belgium                    8343.105127
Bosnia and Herzegovina      973.533195
...
Spain                      3834.034742
Sweden                     8527.844662
Switzerland               14734.232750
Turkey                     1969.100980
United Kingdom             9979.508487
Name: gdpPercap_1952, dtype: float64
~~~
{: .output}

**Keep in mind that the syntax presented in this section represent
shortcuts, which can lead to confusion when first starting out. You
should stick to `.loc` and `.iloc` until you are comfortable
with pandas**

## Result of slicing can be used in further operations.

*   Usually don't just print a slice.
*   All the statistical operators that work on entire dataframes
    work the same way on slices.
*   E.g., calculate max of a slice.

~~~
print(data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'].max())
~~~
{: .python}
~~~
gdpPercap_1962    13450.40151
gdpPercap_1967    16361.87647
gdpPercap_1972    18965.05551
dtype: float64
~~~
{: .output}

~~~
print(data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'].min())
~~~
{: .python}
~~~
gdpPercap_1962    4649.593785
gdpPercap_1967    5907.850937
gdpPercap_1972    7778.414017
dtype: float64
~~~
{: .output}

## Use comparisons to select data based on value.

*   Comparison is applied element by element.
*   Returns a similarly-shaped dataframe of `True` and `False`.

~~~
# Use a subset of data to keep output readable.
subset = data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972']
print('Subset of data:\n', subset)

# Which values were greater than 10000 ?
print('\nWhere are values large?\n', subset > 10000)
~~~
{: .python}
~~~
Subset of data:
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy           8243.582340    10022.401310    12269.273780
Montenegro      4649.593785     5907.850937     7778.414017
Netherlands    12790.849560    15363.251360    18794.745670
Norway         13450.401510    16361.876470    18965.055510
Poland          5338.752143     6557.152776     8006.506993

Where are values large?
            gdpPercap_1962 gdpPercap_1967 gdpPercap_1972
country
Italy                False           True           True
Montenegro           False          False          False
Netherlands           True           True           True
Norway                True           True           True
Poland               False          False          False
~~~
{: .output}

## Select values or NaN using a Boolean mask.

*   A frame full of Booleans is sometimes called a *mask* because of how it can be used.

~~~
mask = subset > 10000
print(subset[mask])
~~~
{: .python}
~~~
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy                   NaN     10022.40131     12269.27378
Montenegro              NaN             NaN             NaN
Netherlands     12790.84956     15363.25136     18794.74567
Norway          13450.40151     16361.87647     18965.05551
Poland                  NaN             NaN             NaN
~~~
{: .output}

*   Get the value where the mask is true, and NaN (Not a Number) where it is false.
*   Useful because NaNs are ignored by operations like max, min, average, etc.

~~~
print(subset[subset > 10000].describe())
~~~
{: .python}
~~~
       gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
count        2.000000        3.000000        3.000000
mean     13120.625535    13915.843047    16676.358320
std        466.373656     3408.589070     3817.597015
min      12790.849560    10022.401310    12269.273780
25%      12955.737547    12692.826335    15532.009725
50%      13120.625535    15363.251360    18794.745670
75%      13285.513523    15862.563915    18879.900590
max      13450.401510    16361.876470    18965.055510
~~~
{: .output}

> ## Selection of Individual Values
>
> Load the Gapminder GDP data for Europe into a dataframe:
>
> ~~~
> europe_df = pandas.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
> ~~~
> {: .python}
>
> Write an expression to find the Per Capita GDP of Serbia in 2007.
>
> > ## Hint
> > 
> > Try using the '`loc`' method
> {: .solution}
>
> > ## Solution
> >
> > ~~~
> > # You can specify a particular peice of data by referencing its coordinate headings
> > print(europe_df.loc["Serbia", "gdpPercap_2007"])
> > ~~~
> > {: .python}
> {: .solution}
{: .challenge}

> ## Extent of Slicing
>
> 1.  Do the two statements below produce the same output?
> 2.  Based on this,
>     what rule governs what is included (or not) in numerical slices and named slices in Pandas?
>
> ~~~
> print(data.iloc[0:2, 0:2])
> print(data.loc['Albania':'Belgium', 'gdpPercap_1952':'gdpPercap_1962'])
> ~~~
> {: .python}
>
> > ## Hint
> > 
> > Try it! Put the statements into a notebook cell.
> {: .solution}
>
> > ## Solution
> >
> > ~~~
> >          gdpPercap_1952  gdpPercap_1957
> > country                                
> > Albania     1601.056136     1942.284244
> > Austria     6137.076492     8842.598030
> >          gdpPercap_1952  gdpPercap_1957  gdpPercap_1962
> > country                                                
> > Albania     1601.056136     1942.284244     2312.888958
> > Austria     6137.076492     8842.598030    10750.721110
> > Belgium     8343.105127     9714.960623    10991.206760
> > ~~~
> > {: .output}
> > Numbered indexing **is not** inclusive of the second half of the slice
> > (i.e., index '2', in this case, is not included), while label 
> > indexing **is** inclusive.
> {: .solution}
{: .challenge}

> ## Reconstructing Data
>
> Explain what each line in the following short program does:
> what is in `first`, `second`, etc.?
>
> ~~~
> first = pandas.read_csv('gapminder/gapminder_all.csv', index_col='country')
> second = first[first['continent'] == 'Americas']
> third = second.drop('Puerto Rico')
> fourth = third.drop('continent', axis = 1)
> fourth.to_csv('result.csv')
> ~~~
> {: .python}
>
> > ## Solution
> >
> > ~~~
> > # Reads a CSV file into a new dataframe
> > first = pandas.read_csv('gapminder/gapminder_all.csv', index_col='country')
> >
> > # Selects only those rows with the value 'Americas' in the 'continent' column 
> > second = first[first['continent'] == 'Americas']
> > 
> > # Remove the 'Puerto Rico' row
> > third = second.drop('Puerto Rico')
> >
> > # Remove the 'continent' column
> > fourth = third.drop('continent', axis = 1)
> >
> > # Write data to a new file
> > fourth.to_csv('result.csv')
> > ~~~
> > {: .python}
> {: .solution}
{: .challenge}

> ## Selecting Indices
>
> Explain in simple terms what `idxmin` and `idxmax` do in the short program below.
> When might you use these methods?
>
> ~~~
> data = pandas.read_csv('gapminder/gapminder_gdp_europe.csv', index_col='country')
> print(data.idxmin())
> print(data.idxmax())
> ~~~
> {: .python}
>
> > ## Hint
> > 
> > Don't forget about the '`help`' method
> > 
> > Compare the output of `print(data.idxmin())` to the output of `print(data)`
> {: .solution}
>
> > ## Solution
> >
> > '`idxmax`' returns the label of the row with the highest value in 
> > each column, and '`idxmin`' returns the minimum.
> > 
> > These methods could be useful when looking for outliers in your data. 
> {: .solution}
{: .challenge}

> ## Practice with Selection
>
> Write an expression to select each of the following from the Europe data:
>
> 1.  GDP per capita for all countries in 1982.
> 1.  GDP per capita for Denmark for all years.
> 1.  GDP per capita for all countries for years *after* 1985.
> 1.  Inflation of GDP per capita for each country between 2007 and 1952 (i.e., 2007 divided by 1952).
>
> > ## Hint
> > 
> > Everything can be done with the '`loc`' method
> {: .solution}
>
> > ## Solution
> >
> > ~~~
> > # GDP per capita for all countries in 1982.
> > europe_df.loc[:, "gdpPercap_1982"]
> >
> > # GDP per capita for Denmark for all years.
> > europe_df.loc["Denmark", :]
> > 
> > # GDP per capita for all countries for years *after* 1985.
> > europe_df.loc[:, "gdpPercap_1985":]
> >
> > # GDP per capita for each country in 2007 as a multiple of GDP per capita for that country in 1952.
> > europe_df.loc[:, "gdpPercap_2007"] / europe_df.loc[:, "gdpPercap_1952"]
> > ~~~
> > {: .python}
> {: .solution}
{: .challenge}

<!--
> ## Processing Small Files
>
> Modify this program so that it only processes files with fewer than 50 records.
>
> ~~~
> import glob
> import pandas
> for filename in glob.glob('data/*.csv'):
>     contents = pandas.read_csv(filename)
>     ____:
>         print(filename, len(contents))
> ~~~
> {: .python}
{: .challenge}

> ## Interpretation
>
> Poland's borders have been stable since 1945,
> but changed several times in the years before then.
> How would you handle this if you were creating a table of GDP per capita for Poland
> for the entire Twentieth Century?
{: .challenge}


> ## 'Applying' a function to a Pandas DataFrame
>
> Consider the following:
>
> ~~~
> def economic_status(gdp_per_capita):
>     if value < 11450:
>         return "poor"
>     elif value < 20900:
>         return "middle"
>     elif value >= 20900:
>         return "rich"
>     else:
>         # This observation has bad data
>         return None
>
> print(europe_df["gdpPercap_1982"].head(5))
>
> for indx, gdp in enumerate(europe_df["gdpPercap_1982"]):
>     europe_df["gdpPercap_1982"][indx] = economic_status(gdp)
>
> print(europe_df["gdpPercap_1982"].head(5))
> ~~~
> {: .python}
>
> ~~~
> 2
> ~~~
> {: .output}
>
> That function would typically be used within a `for` loop, but Pandas has
> a different, more efficient way of doing the same thing, and that is by
> *applying* a function to a dataframe or a portion of a dataframe.  Here
> is an example, using the definition above.
>
> ~~~
> data = pd.read_csv('Americas-data.csv')
> data['life_qrtl'] = data['lifeExp'].apply(calculate_life_quartile)
> ~~~
> {: .python}
>
> There is a lot in that second line, so let's take it piece by piece.
>
> On the right side of the '`=`' we start with `data['lifeExp']`, which is the
> column in the dataframe called '`data`' labeled '`lifExp`'.  We use the
> `apply()` to do what it says, apply the '`calculate_life_quartile`' to the
> value of this column for every row in the dataframe.
{: .challenge}
-->