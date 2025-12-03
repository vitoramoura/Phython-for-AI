# Exercise Solutions

This document gathers solutions for all exercises and questions across the workshop notebooks. Code snippets assume the surrounding context established in each notebook (e.g., imports, data loading, and existing variables) and are ready to paste into the matching code cells.

## 01_brief_intro_python.ipynb

### Exercise 1
```python
first_name = "Ada"
```

### Exercise 2
```python
result = (100 - 5**3) / 5
# result == -5.0
```

### Exercise 3
```python
value = 15 / 4 + 6
# value == 9.75
```

### Exercise 4
```python
x = 3.14
print(type(x))  # <class 'float'>
```

### Exercise 5 + Question
```python
x = 3.14
y = int(x)
print(type(y))  # <class 'int'>
print(y)        # 3

# Question: Did Python round 3.14 when casting to int?
# Answer: No. int() truncates toward zero. For example:
z = 7.92
print(int(z))   # 7
```

### Exercise 6
```python
y = 3
z = float(y)
print(type(z))  # <class 'float'>
print(z)        # 3.0
```

### Exercise 7
```python
def add(x, y):
    """Return the sum of x and y."""
    return x + y
```

### Exercise 8
```python
sum_result = add(12, 30)
print(sum_result)  # 42
```

### Exercise 9
```python
def square(number):
    """Return the square of the provided number."""
    return number ** 2

print(square(6))  # 36
```

## 02_data_analysis_pandas.ipynb
Before starting the exercises, load the Gapminder data as shown in the notebook so you have a DataFrame `df` ready for use:

```python
import pandas as pd

df = pd.read_csv("data/gapminder.csv")
```

Solutions below assume `df` is available and filtered where appropriate.

### Exercise 1
```python
df.head()
```

### Exercise 2
```python
df.head(10)
```

### Exercise 3
```python
df.tail()
```

### Exercise 4
```python
df.tail(10)
```

### Exercise 5
```python
df['gdpPercap_2007']
```

### Exercise 6
```python
df[['gdpPercap_2007', 'lifeExp_2007', 'pop_2007']]
```

### Exercise 7
```python
df3 = df.drop(columns=['continent'])
df3.head()
```

### Exercise 8
```python
df['gdpPercap_2007'].min()
```

### Exercise 9
```python
df['gdpPercap_2007'].max()
```

### Exercise 10
```python
df[df['gdpPercap_2007'] < 500]
```

### Exercise 11
```python
df[df['continent'] == 'Europe'].head()
```

### Exercise 12
```python
df[(df['continent'] == 'Europe') & (df['lifeExp_2007'] > 80)]
```

### Exercise 13
```python
from plotnine import ggplot, aes, geom_histogram

(
    ggplot(df)
    + aes(x='lifeExp_2007')
    + geom_histogram(binwidth=2)
)
```

### Exercise 14
```python
from plotnine import ggplot, aes, geom_histogram, geom_boxplot, facet_wrap

# Example: histogram of 2007 GDP per capita for countries with population over 10 million
ggplot(df[df['pop_2007'] > 10_000_000]) + aes(x='gdpPercap_2007') + geom_histogram(binwidth=2000)

# Example: boxplots of life expectancy by continent
(
    ggplot(df)
    + aes(x='continent', y='lifeExp_2007')
    + geom_boxplot()
)
```

### Exercise 15
```python
from plotnine import ggplot, aes, geom_histogram, labs

(
    ggplot(df)
    + aes(x='gdpPercap_2007')
    + geom_histogram(binwidth=1000, fill='#4C72B0', color='black')
    + labs(x='Gross Domestic Product Per Capita, 2007', y='Count')
)
```

### Exercise 16
```python
from plotnine import ggplot, aes, geom_point, geom_smooth, labs, theme_minimal

(
    ggplot(df)
    + aes(x='gdpPercap_2007', y='lifeExp_2007', color='continent', size='pop_2007')
    + geom_point(alpha=0.6)
    + geom_smooth(method='loess', se=False)
    + labs(x='GDP per Capita (2007)', y='Life Expectancy (2007)', title='Life Expectancy vs GDP per Capita')
    + theme_minimal()
)
```

## 03_what_went_wrong.ipynb

This notebook does not contain dedicated exercise blocks; instead, it focuses on debugging concepts. No standalone solutions are required.

## 04_more_data_visualization.ipynb
Load the energy consumption data into a DataFrame named `energy` before running the plotting solutions. The notebook uses the file `data/Figure5_2.csv` and keeps the column names `year`, `source`, and `value` (QBTU):

```python
import pandas as pd

energy = pd.read_csv('data/Figure5_2.csv')
```

If you want to reuse the same colors shown in the notebook, define the palette used in the examples:

```python
palette = {
    'Coal': '#00BFC4',
    'Natural Gas': '#F8766D',
    'Nuclear': '#7CAE00',
    'Petroleum': '#C77CFF',
}
```

### Exercise 1
```python
from plotnine import ggplot, aes, geom_line, labs

(
    ggplot(energy[energy['source'] == 'Natural Gas'])
    + aes(x='year', y='value')
    + geom_line(color='#F8766D', size=1.1)
    + labs(title='U.S. Natural Gas Consumption', x='Year', y='QBTU')
)
```

### Exercise 2
```python
from plotnine import ggplot, aes, geom_line, labs, theme_bw

(
    ggplot(energy[energy['source'] == 'Coal'])
    + aes(x='year', y='value')
    + geom_line(color='#00BFC4', size=1.3)
    + labs(
        title='Coal Consumption Over Time',
        x='Year',
        y='Energy Consumption (QBTU)'
    )
    + theme_bw()
)
```
