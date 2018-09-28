
## Lambda Functions

Lambda functions are often a convenient way to write *throw away* functions on the fly. If you need to write a more complicated function you may still need to use the more formal `def` method, but lambda functions provide a quick and concise way to write functions. For example, let's say you want to count the number of words in each yelp review.


```python
import pandas as pd
df = pd.read_csv('Yelp_Reviews.csv')
df.head(2)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>business_id</th>
      <th>cool</th>
      <th>date</th>
      <th>funny</th>
      <th>review_id</th>
      <th>stars</th>
      <th>text</th>
      <th>useful</th>
      <th>user_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>pomGBqfbxcqPv14c3XH-ZQ</td>
      <td>0</td>
      <td>2012-11-13</td>
      <td>0</td>
      <td>dDl8zu1vWPdKGihJrwQbpw</td>
      <td>5</td>
      <td>I love this place! My fiance And I go here atl...</td>
      <td>0</td>
      <td>msQe1u7Z_XuqjGoqhB0J5g</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>jtQARsP6P-LbkyjbO1qNGg</td>
      <td>1</td>
      <td>2014-10-23</td>
      <td>1</td>
      <td>LZp4UX5zK3e-c5ZGSeo3kA</td>
      <td>1</td>
      <td>Terrible. Dry corn bread. Rib tips were all fa...</td>
      <td>3</td>
      <td>msQe1u7Z_XuqjGoqhB0J5g</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['text'].map(lambda x: len(x.split())).head()
```




    0    58
    1    30
    2    30
    3    82
    4    32
    Name: text, dtype: int64



Similar to defining functions in general or naming the iterable in for loops, the variable that you use after calling the `lambda` keyword does not matter


```python
df['text'].map(lambda review_text: len(review_text.split())).head()
```




    0    58
    1    30
    2    30
    3    82
    4    32
    Name: text, dtype: int64



# Lambda functions with conditionals
Lambda functions can also accept some conditionals if chained in a list comprehension


```python
df['text'].map(lambda x: 'Good' if any([word in x.lower() for word in ['awesome', 'love', 'good', 'great']]) else 'Bad').head()
```




    0    Good
    1     Bad
    2    Good
    3     Bad
    4     Bad
    Name: text, dtype: object



# Note: 
The above is terribly poor style and does in no way represent [pep-8](https://www.python.org/dev/peps/pep-0008/) or pythonic style. (For example, no line should be over 72 characters according to pep-8; the previous line was 127 characters.) That said, it is an interesting demonstration of chaining a conditional, the any method and a list comprehension all inside a lambda function!   
Shew!

# Returning to a more manageable example...

Perhaps we want to naively select the year from the date string rather then convert it to a datetime object.


```python
df.date.map(lambda x: x[:4]).head()
```




    0    2012
    1    2014
    2    2014
    3    2011
    4    2016
    Name: date, dtype: object



# Lambda Functions are also useful within the sort method



```python
#Without a key
names = ['Miriam Marks','Sidney Baird','Elaine Barrera','Eddie Reeves','Marley Beard',
         'Jaiden Liu','Bethany Martin','Stephen Rios','Audrey Mayer','Kameron Davidson',
         'Carter Wong','Teagan Bennett']
sorted(names)
```




    ['Audrey Mayer',
     'Bethany Martin',
     'Carter Wong',
     'Eddie Reeves',
     'Elaine Barrera',
     'Jaiden Liu',
     'Kameron Davidson',
     'Marley Beard',
     'Miriam Marks',
     'Sidney Baird',
     'Stephen Rios',
     'Teagan Bennett']




```python
#Sorting by last name
names = ['Miriam Marks','Sidney Baird','Elaine Barrera','Eddie Reeves','Marley Beard',
         'Jaiden Liu','Bethany Martin','Stephen Rios','Audrey Mayer','Kameron Davidson',
'Teagan Bennett']
sorted(names, key=lambda x: x.split()[1])

```




    ['Sidney Baird',
     'Elaine Barrera',
     'Marley Beard',
     'Teagan Bennett',
     'Kameron Davidson',
     'Jaiden Liu',
     'Miriam Marks',
     'Bethany Martin',
     'Audrey Mayer',
     'Eddie Reeves',
     'Stephen Rios']




```python

```
