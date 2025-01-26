```python
import pandas as pd
```

```python
df = pd.read_csv('Data.csv')
df
```

```python
df.head(10)
```

```python
df.tail(10)
```

```python
df.shape
```

```python
print('Number of Rows',df.shape[0])
print('Number of Columns',df.shape[1])
```

```
Number of Rows 1000
Number of Columns 12

```

```python
df.info()
```

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1000 entries, 0 to 999
Data columns (total 12 columns):
 #   Column              Non-Null Count  Dtype  
---  ------              --------------  -----  
 0   Rank                1000 non-null   int64  
 1   Title               1000 non-null   object 
 2   Genre               1000 non-null   object 
 3   Description         1000 non-null   object 
 4   Director            1000 non-null   object 
 5   Actors              1000 non-null   object 
 6   Year                1000 non-null   int64  
 7   Runtime (Minutes)   1000 non-null   int64  
 8   Rating              1000 non-null   float64
 9   Votes               1000 non-null   int64  
 10  Revenue (Millions)  872 non-null    float64
 11  Metascore           936 non-null    float64
dtypes: float64(3), int64(4), object(5)
memory usage: 93.9+ KB

```

```python
df.describe()
```

```python
df.describe(include="all")
```

```python
df.isnull().sum()
```

```python
import matplotlib.pyplot as plt
import seaborn as sns
sns.heatmap(df.isnull())
plt.show()
```

```python
df = df.dropna(axis=0)
```

```python
sns.heatmap(df.isnull())
plt.show()
```

```python
dup_data=df.duplicated().any()
print("Are there any duplicated values in data?",dup_data)
```

```
Are there any duplicated values in data? False

```

```python
df[df['Runtime (Minutes)']>=180]['Title']
```

```python
sns.barplot(x='Year',y='Votes',data=df)
plt.title("Votes By Year")
plt.show()
```

```python
le =df.nlargest(10,'Runtime (Minutes)')[['Title','Runtime (Minutes)']]. \
set_index('Title')
```

```python
sns.barplot(x='Year',y='Revenue (Millions)',data=df)
plt.title("Revenue By Year")
plt.show()
```

```python
df.groupby('Director')['Rating'].mean().sort_values(ascending=False)
```

```python
data = le[['Runtime (Minutes)']].copy()
data['Movie'] = le.index
sns.barplot(x='Runtime (Minutes)', y='Movie', data=data)
plt.title('Top 5 Lengthy Movies')
plt.show()

```

```python
sns.countplot(x='Year',data=df)
plt.title("Number of Movies Per Year")
```

```python
df.columns
```

```python
df[df['Revenue (Millions)'].max() == df['Revenue (Millions)']]['Title']
```

```python
top_10=df.nlargest(10,'Rating')[['Title','Rating','Director']].set_index('Title')
top_10
```

```python
sns.barplot(x=top_10['Rating'], y=top_10.index)
plt.title("Display Top 10 Highest Rated Movie Titles")
plt.show()
```

```python
df.sort_values(by='Revenue (Millions)',ascending=False).head(10)
```

```python
top_10 = df.nlargest(10,'Revenue (Millions)')[['Title','Director','Revenue (Millions)']].set_index('Title')
```

```python
sns.barplot(x=top_10['Revenue (Millions)'], y=top_10.index)
plt.title("Display Top 10 Highest Revenue Movie Titles")
plt.show()
```

```python
data1 = (
    df.groupby('Year')[['Rating']]
    .mean()
    .sort_values(by='Rating', ascending=False)
)


```

```python
data1
```

```python
sns.scatterplot(x='Rating',y='Revenue (Millions)',data=df)
```

```python
def rating(rating):
    if rating>=7.0:
        return 'Excellent'
    elif rating>=6.0:
        return 'Good'
    else:
        return 'Average'
```

```python
df['rating_cat']=df['Rating'].apply(rating)
```

```python
df.head(1)
```

```python
list1 = [value.split(',') for value in df['Genre']]

```

```python
list1
```

```python
df['Rating'].value_counts().plot(kind="pie")
```

```python
df['Rating'].value_counts().plot(kind="line")
```

```python
df['Rating'].value_counts().plot(kind="bar")
```

```python
df['Year'].value_counts().plot(kind="bar")
```

```python

```