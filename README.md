# Data Engineering Assignment

### Importing panadas Libariy and giving them a alias name

```python
import pandas as pd
import matplotlib.pyplot as plt
```


### Reading CSV File
```python
df = pd.read_csv('netflix_titles.csv')
df.head()
```
#### Question #1: Convert dates into a proper date-time format of your choice
```python
df['date_added'] = pd.to_datetime(df['date_added'])
```

#### Question #2: Finding seasons count from durations columns
Removing all NaN values
```python
df = df.dropna(how='any')
```

First find the 'season' word from duration column
```python
s=df['duration'].str.find('Season')

``
Then add a new column named as 'seasons'
```python
df['s'] = df['duration'].str.find('Season')
```
Counting the duration with the value of seasons
```python
df[df['season'] != -1].count()
```

#### Question #5: How many movies were released each year.
5.1 Get the all movies from type column and get into movie_year
```python
movie_year = df[df['type'] == 'Movie']
```
Here apply the groupby function on release_year column and calculate the count
```python
movie_year.groupby(['release_year']).count()
```

#### Question #6: Which month is the best month to release it.
Adding a extra colomn as the month column and take the month from date_added column
```python
df['month'] = pd.DatetimeIndex(df['date_added']).month
```
Convert the month datatype into int from float
```python
df['month'] = df['month'].astype('int32')

counting the released Movie from release_year and groupby with month column
```python
result = df[['month','show_id']].groupby(['month']).count()
result
```

6.4 And output with pie chart using matplotlib library
```python
from matplotlib import pyplot as plt
import numpy as np
fig = plt.figure()
ax = fig.add_axes([0,0,1,1])
ax.axis('equal')
langs = ['Jan', 'Fab', 'March', 'April', 'May','June','July','Aug','Sep','oct','Nov','Dec']
students = [489,341,469,471,368,415,464,449,427,491,458,490]
ax.pie(students, labels = langs,autopct='%1.2f%%')
plt.show()
```

#### Output in HTML File
```python
df.to_html('gd.html')
```
