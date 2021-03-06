---
layout: post
title: 주피터 노트북
comments: true
categories: [Data Science/Statistics]
tags: [Statistics,JupyterNotebook,Pandas,Numpy]
---
<br>

# <center> Pandas </center>

<br>

### 1. pandas로 데이터 가져오기


```python
import pandas as pd   # pandas 패키지 불러오기
import numpy as np    # numpy 패키지 불러오기
```

> pandas로 csv파일 불러오기


```python
df = pd.read_csv('bank_customer.csv')
```


```python
df #  실행시 전체 dataSet 출력
```

> 불러온 csv파일 확인


```python
df.info()
# df.index()  # indext에 대한 세부정보 (! 기본RangeIndex는 안됨)  
# df.columns  # columns 세부정보
# df.values
```

> 9개의 column(index 제외) , column별 row, null값 여부, dataType 확인


```python
df.head(10)  #  맨위에서 부터 10개 출력
# df.tail(10)  # 맨아래에서 부터 10개 출력
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
      <th>cid</th>
      <th>age</th>
      <th>job</th>
      <th>marital</th>
      <th>education</th>
      <th>default</th>
      <th>balance</th>
      <th>housing</th>
      <th>loan</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>C00004</td>
      <td>47</td>
      <td>blue-collar</td>
      <td>married</td>
      <td>NaN</td>
      <td>no</td>
      <td>1506</td>
      <td>yes</td>
      <td>no</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C00005</td>
      <td>33</td>
      <td>NaN</td>
      <td>single</td>
      <td>NaN</td>
      <td>no</td>
      <td>1</td>
      <td>no</td>
      <td>no</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C00009</td>
      <td>58</td>
      <td>retired</td>
      <td>married</td>
      <td>1.0</td>
      <td>no</td>
      <td>121</td>
      <td>yes</td>
      <td>no</td>
    </tr>
    <tr>
      <th>3</th>
      <td>C00021</td>
      <td>28</td>
      <td>blue-collar</td>
      <td>married</td>
      <td>2.0</td>
      <td>no</td>
      <td>723</td>
      <td>yes</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>4</th>
      <td>C00025</td>
      <td>40</td>
      <td>retired</td>
      <td>married</td>
      <td>1.0</td>
      <td>no</td>
      <td>0</td>
      <td>yes</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>5</th>
      <td>C00026</td>
      <td>44</td>
      <td>admin.</td>
      <td>married</td>
      <td>2.0</td>
      <td>no</td>
      <td>-372</td>
      <td>yes</td>
      <td>no</td>
    </tr>
    <tr>
      <th>6</th>
      <td>C00027</td>
      <td>39</td>
      <td>management</td>
      <td>single</td>
      <td>3.0</td>
      <td>no</td>
      <td>255</td>
      <td>yes</td>
      <td>no</td>
    </tr>
    <tr>
      <th>7</th>
      <td>C00029</td>
      <td>46</td>
      <td>management</td>
      <td>single</td>
      <td>2.0</td>
      <td>no</td>
      <td>-246</td>
      <td>yes</td>
      <td>no</td>
    </tr>
    <tr>
      <th>8</th>
      <td>C00031</td>
      <td>57</td>
      <td>technician</td>
      <td>married</td>
      <td>2.0</td>
      <td>no</td>
      <td>839</td>
      <td>no</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>9</th>
      <td>C00035</td>
      <td>51</td>
      <td>management</td>
      <td>married</td>
      <td>3.0</td>
      <td>no</td>
      <td>10635</td>
      <td>yes</td>
      <td>no</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.T # 데이터 전치 ( Columns <-> index )
```


```python
df.sort_index(ascending=True) # ascending = False
```

> 데이터 오름차순,내림차순 정렬 (index 기준)


```python
df.sort_values(by='age',ascending=False)
```

> 데이터 값 기준으로 정렬(특정 column 선택)

### 2. Data Selection


```python
# df['age']
df[['age','cid']]  # 다중선택 => [[]]

# df.loc[[0,10]]
```

> column 선택하기


```python
df[0:10] # 0~9 행 슬라이스  ## df.loc[0:10]
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
      <th>cid</th>
      <th>age</th>
      <th>job</th>
      <th>marital</th>
      <th>education</th>
      <th>default</th>
      <th>balance</th>
      <th>housing</th>
      <th>loan</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>C00004</td>
      <td>47</td>
      <td>blue-collar</td>
      <td>married</td>
      <td>NaN</td>
      <td>no</td>
      <td>1506</td>
      <td>yes</td>
      <td>no</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C00005</td>
      <td>33</td>
      <td>NaN</td>
      <td>single</td>
      <td>NaN</td>
      <td>no</td>
      <td>1</td>
      <td>no</td>
      <td>no</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C00009</td>
      <td>58</td>
      <td>retired</td>
      <td>married</td>
      <td>1.0</td>
      <td>no</td>
      <td>121</td>
      <td>yes</td>
      <td>no</td>
    </tr>
    <tr>
      <th>3</th>
      <td>C00021</td>
      <td>28</td>
      <td>blue-collar</td>
      <td>married</td>
      <td>2.0</td>
      <td>no</td>
      <td>723</td>
      <td>yes</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>4</th>
      <td>C00025</td>
      <td>40</td>
      <td>retired</td>
      <td>married</td>
      <td>1.0</td>
      <td>no</td>
      <td>0</td>
      <td>yes</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>5</th>
      <td>C00026</td>
      <td>44</td>
      <td>admin.</td>
      <td>married</td>
      <td>2.0</td>
      <td>no</td>
      <td>-372</td>
      <td>yes</td>
      <td>no</td>
    </tr>
    <tr>
      <th>6</th>
      <td>C00027</td>
      <td>39</td>
      <td>management</td>
      <td>single</td>
      <td>3.0</td>
      <td>no</td>
      <td>255</td>
      <td>yes</td>
      <td>no</td>
    </tr>
    <tr>
      <th>7</th>
      <td>C00029</td>
      <td>46</td>
      <td>management</td>
      <td>single</td>
      <td>2.0</td>
      <td>no</td>
      <td>-246</td>
      <td>yes</td>
      <td>no</td>
    </tr>
    <tr>
      <th>8</th>
      <td>C00031</td>
      <td>57</td>
      <td>technician</td>
      <td>married</td>
      <td>2.0</td>
      <td>no</td>
      <td>839</td>
      <td>no</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>9</th>
      <td>C00035</td>
      <td>51</td>
      <td>management</td>
      <td>married</td>
      <td>3.0</td>
      <td>no</td>
      <td>10635</td>
      <td>yes</td>
      <td>no</td>
    </tr>
  </tbody>
</table>
</div>



> 슬라이스


```python
# df[20130101 : 20150202]
```

> range index뿐만 아니라 날짜 인덱스 등 다양한 형식 가능 <br>
> 만약 index가 2013-05-02 인 경우 pandas에서 자동으로 20130502로 인식

#### 2.1 loc,iloc Indexing

> dataframe.loc[행,열] <br><br>
loc[] 에 값을 하나만 넣는 경우 row 선택 <br>


```python
# df.loc[3]        # index가 3인 row의 값들을 선택
# df.loc[0:3]      # index 0~2 슬라이싱
# df.loc[[0,3]]
```


```python
# df.age >300
df.loc[ df.age > 300 ]   # boolean 활용 loc 슬라이싱
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
      <th>cid</th>
      <th>age</th>
      <th>job</th>
      <th>marital</th>
      <th>education</th>
      <th>default</th>
      <th>balance</th>
      <th>housing</th>
      <th>loan</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7788</th>
      <td>C25900</td>
      <td>380</td>
      <td>management</td>
      <td>single</td>
      <td>3.0</td>
      <td>no</td>
      <td>1998</td>
      <td>no</td>
      <td>no</td>
    </tr>
  </tbody>
</table>
</div>
