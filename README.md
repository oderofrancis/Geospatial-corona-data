# Geospatial Corona Data

## Geopandas and Pandas

To merge two dataframes using pandas, you can use the pd.merge() function. This function allows you to merge two dataframes by specifying columns in each dataframe as keys. For example:

```python

import pandas as pd

df1 = pd.DataFrame({'key': ['K0', 'K1', 'K2', 'K3'],
                     'A': ['A0', 'A1', 'A2', 'A3'],
                     'B': ['B0', 'B1', 'B2', 'B3']})

df2 = pd.DataFrame({'key': ['K0', 'K1', 'K2', 'K3'],
                     'C': ['C0', 'C1', 'C2', 'C3'],
                     'D': ['D0', 'D1', 'D2', 'D3']})

result = pd.merge(df1, df2, on='key')
print(result)

```

This would output the following dataframe:

```python
key   A   B   C   D
0  K0  A0  B0  C0  D0
1  K1  A1  B1  C1  D1
2  K2  A2  B2  C2  D2
3  K3  A3  B3  C3  D3
```

You can specify different merge options using the how parameter. For example, you can use how='inner' to specify an inner join, how='left' for a left join, and how='right' for a right join.

You can also specify the columns to join on using the left_on and right_on parameters if the column names are different in each dataframe.

Geopandas has a geopandas.GeoDataFrame.merge() function that is similar to the pd.merge() function in pandas. You can use this function to merge two geopandas dataframes by specifying columns in each dataframe as keys.

Here is an example of how to use geopandas.GeoDataFrame.merge():

```python
import geopandas as gpd

# Load two geopandas dataframes
df1 = gpd.read_file('data1.shp')
df2 = gpd.read_file('data2.shp')

# Merge the dataframes on the 'key' column
result = df1.merge(df2, on='key')

```
The geopandas.GeoDataFrame.merge() function has the same parameters as the pd.merge() function, such as how, left_on, and right_on, which allow you to specify different merge options and columns to join on.

What about you have a dataframe with geometry column and the other one doesn't have ?

In this case use pandas to merge the two dataframe using the commom column the convert the results to geodataframe.

To convert a pandas dataframe to a geopandas dataframe, you will need to create a GeoDataFrame object and set the geometry column of the dataframe to the geometry attribute of the GeoDataFrame.

Here is an example of how to do this:

```python
import geopandas as gpd

# Load a pandas dataframe
df1 = pd.read_csv('data1.csv')

df2 = pd.read_csv('data2.csv')

# use common column name

result = df1.merge(df2, on='name')

# Create a GeoDataFrame
gdf = gpd.GeoDataFrame(result, geometry='geometry')

```

n this example, we are using the Point geometry from the shapely library to create a geometry column in the dataframe. The apply() function is used to apply the Point function to each row in the dataframe, and the resulting Point objects are stored in the geometry column.

Once the geometry column has been created, we can create a GeoDataFrame by passing the dataframe and the geometry column name to the gpd.GeoDataFrame() constructor.
