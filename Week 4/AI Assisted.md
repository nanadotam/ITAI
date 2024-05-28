# AI Assisted
Sure, let's go through the steps needed to complete your assignment using Python and pandas.

### Step 1: Web Scraping

To scrape the data from the web page, you'll need to use the BeautifulSoup and requests libraries. Assuming the data is available in a structured HTML table on the page, the following code can be used to scrape it:

```python
import requests
from bs4 import BeautifulSoup
import pandas as pd

# URL of the webpage containing the table of presidents
url = "<https://en.wikipedia.org/wiki/List_of_presidents_of_the_United_States>"

# Sending a request to the webpage
response = requests.get(url)

# Parsing the content of the webpage
soup = BeautifulSoup(response.content, 'html.parser')

# Finding the table in the webpage
table = soup.find('table', {'class': 'wikitable'})

# Reading the table into a pandas dataframe
df = pd.read_html(str(table))[0]

# Display the dataframe to verify the data
print(df.head())

```

### Step 2: Data Preparation and Analysis

Let's perform the required tasks using pandas:

1. **How many presidents are on the web page?**

```python
num_presidents = df['President'].nunique()
print(f"Number of presidents: {num_presidents}")

```

1. **How many presidencies ever existed in the United States?**

```python
num_presidencies = len(df)
print(f"Number of presidencies: {num_presidencies}")

```

1. **Which presidents served more than one term and had only one vice president for the whole duration of their presidency?**

```python
more_than_one_term = df[df['Presidency'].str.contains("Term")]
single_vp = more_than_one_term[more_than_one_term['Vice President'].str.split(',').apply(len) == 1]
print(single_vp[['President', 'Vice President']])

```

1. **Which president was in office longer than others and when did he get in office?**

```python
df['Term length (years)'] = df['Term in office'].apply(lambda x: int(x.split('–')[1]) - int(x.split('–')[0]))
longest_serving_president = df[df['Term length (years)'] == df['Term length (years)'].max()]
print(longest_serving_president[['President', 'Term in office']])

```

1. **Which presidents were elected after serving as vice presidents?**

```python
vice_presidents = df[df['Previous office'].str.contains('Vice President', na=False)]
print(vice_presidents[['President', 'Previous office']])

```

1. **Which presidents were elected after serving as senators?**

```python
senators = df[df['Previous office'].str.contains('Senator', na=False)]
print(senators[['President', 'Previous office']])

```

1. **How many presidents have the same forenames and/or surnames and who are they?**

```python
same_forenames = df['President'].apply(lambda x: x.split(' ')[0]).value_counts()
same_surnames = df['President'].apply(lambda x: x.split(' ')[-1]).value_counts()
print("Presidents with the same forenames:")
print(same_forenames[same_forenames > 1])
print("Presidents with the same surnames:")
print(same_surnames[same_surnames > 1])

```

1. **Who was the oldest president ever elected for office?**

```python
oldest_president = df.loc[df['Age at inauguration'].idxmax()]
print(f"Oldest president: {oldest_president['President']}")

```

1. **Who was the youngest president ever elected for office?**

```python
youngest_president = df.loc[df['Age at inauguration'].idxmin()]
print(f"Youngest president: {youngest_president['President']}")

```

1. **Which president lived up to a very old age, after leaving office?**

```python
df['Age at death'] = df['Death year'] - df['Birth year']
oldest_after_office = df.loc[df['Age at death'].idxmax()]
print(f"President who lived longest after office: {oldest_after_office['President']}")

```

1. **Draw a graph that shows the number of presidents and their respective political parties which they came from, and which party have many elected presidents?**

```python
import matplotlib.pyplot as plt

party_counts = df['Political party'].value_counts()
party_counts.plot(kind='bar')
plt.title('Number of Presidents by Political Party')
plt.xlabel('Political Party')
plt.ylabel('Number of Presidents')
plt.show()

```

Make sure to adjust the column names and data handling based on the exact structure of the data you scrape from the webpage. This code should give you a good starting point for your analysis.

---

Sure, let's go through the steps needed to complete your assignment using Python and pandas.

### Step 1: Web Scraping

To scrape the data from the web page, you'll need to use the BeautifulSoup and requests libraries. Assuming the data is available in a structured HTML table on the page, the following code can be used to scrape it:

```python
import requests
from bs4 import BeautifulSoup
import pandas as pd

# URL of the webpage containing the table of presidents
url = "<https://en.wikipedia.org/wiki/List_of_presidents_of_the_United_States>"

# Sending a request to the webpage
response = requests.get(url)

# Parsing the content of the webpage
soup = BeautifulSoup(response.content, 'html.parser')

# Finding the table in the webpage
table = soup.find('table', {'class': 'wikitable'})

# Reading the table into a pandas dataframe
df = pd.read_html(str(table))[0]

# Display the dataframe to verify the data
print(df.head())

```

### Step 2: Data Preparation and Analysis

Let's perform the required tasks using pandas:

1. **How many presidents are on the web page?**

```python
num_presidents = df['President'].nunique()
print(f"Number of presidents: {num_presidents}")

```

1. **How many presidencies ever existed in the United States?**

```python
num_presidencies = len(df)
print(f"Number of presidencies: {num_presidencies}")

```

1. **Which presidents served more than one term and had only one vice president for the whole duration of their presidency?**

```python
more_than_one_term = df[df['Presidency'].str.contains("Term")]
single_vp = more_than_one_term[more_than_one_term['Vice President'].str.split(',').apply(len) == 1]
print(single_vp[['President', 'Vice President']])

```

1. **Which president was in office longer than others and when did he get in office?**

```python
df['Term length (years)'] = df['Term in office'].apply(lambda x: int(x.split('–')[1]) - int(x.split('–')[0]))
longest_serving_president = df[df['Term length (years)'] == df['Term length (years)'].max()]
print(longest_serving_president[['President', 'Term in office']])

```

1. **Which presidents were elected after serving as vice presidents?**

```python
vice_presidents = df[df['Previous office'].str.contains('Vice President', na=False)]
print(vice_presidents[['President', 'Previous office']])

```

1. **Which presidents were elected after serving as senators?**

```python
senators = df[df['Previous office'].str.contains('Senator', na=False)]
print(senators[['President', 'Previous office']])

```

1. **How many presidents have the same forenames and/or surnames and who are they?**

```python
same_forenames = df['President'].apply(lambda x: x.split(' ')[0]).value_counts()
same_surnames = df['President'].apply(lambda x: x.split(' ')[-1]).value_counts()
print("Presidents with the same forenames:")
print(same_forenames[same_forenames > 1])
print("Presidents with the same surnames:")
print(same_surnames[same_surnames > 1])

```

1. **Who was the oldest president ever elected for office?**

```python
oldest_president = df.loc[df['Age at inauguration'].idxmax()]
print(f"Oldest president: {oldest_president['President']}")

```

1. **Who was the youngest president ever elected for office?**

```python
youngest_president = df.loc[df['Age at inauguration'].idxmin()]
print(f"Youngest president: {youngest_president['President']}")

```

1. **Which president lived up to a very old age, after leaving office?**

```python
df['Age at death'] = df['Death year'] - df['Birth year']
oldest_after_office = df.loc[df['Age at death'].idxmax()]
print(f"President who lived longest after office: {oldest_after_office['President']}")

```

1. **Draw a graph that shows the number of presidents and their respective political parties which they came from, and which party have many elected presidents?**

```python
import matplotlib.pyplot as plt

party_counts = df['Political party'].value_counts()
party_counts.plot(kind='bar')
plt.title('Number of Presidents by Political Party')
plt.xlabel('Political Party') 
plt.ylabel('Number of Presidents')
plt.show()

```

Make sure to adjust the column names and data handling based on the exact structure of the data you scrape from the webpage. This code should give you a good starting point for your analysis.
