---
layout: post
title: 판다스 Basic
comments: true
categories: [Python/Pandas]
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

<br>
> pandas로 csv파일 불러오기 <br>


```python
df = pd.read_csv('bank_customer.csv')
```


```python
df #  실행시 전체 dataSet 출력
```


> 불러온 csv파일 확인 <br>


```python
df.info()
# df.index()  # indext에 대한 세부정보 (! 기본RangeIndex는 안됨)  
# df.columns  # columns 세부정보
# df.values
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 13563 entries, 0 to 13562
    Data columns (total 9 columns):
    cid          13563 non-null object
    age          13563 non-null int64
    job          13476 non-null object
    marital      13563 non-null object
    education    12995 non-null float64
    default      13563 non-null object
    balance      13563 non-null int64
    housing      13563 non-null object
    loan         13563 non-null object
    dtypes: float64(1), int64(2), object(6)
    memory usage: 953.7+ KB



> 9개의 column(index 제외) , column별 row, null값 여부, dataType 확인 <br>


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


> 데이터 오름차순,내림차순 정렬 (index 기준) <br>


```python
df.sort_values(by='age',ascending=False)
```


> 데이터 값 기준으로 정렬(특정 column 선택) <br><br>

### 2. Data Selection
<br><br>


```python
# df['age']
df[['age','cid']]  # 다중선택 => [[]]

# df.loc[[0,10]]
```

> column 선택하기
<br>


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



> 슬라이스 <br>


```python
# df[20130101 : 20150202]
```

> range index뿐만 아니라 날짜 인덱스 등 다양한 형식 가능 <br>
> 만약 index가 2013-05-02 인 경우 pandas에서 자동으로 20130502로 인식
<br>

<br>
####  2.1 loc,iloc
<br>

> dataframe.loc[행,열] <br><br>
loc[] 에 값을 하나만 넣는 경우 row 선택 <br>
<br>
> iloc는 정수형으로(몇번째부터 몇번째)으로 접근가능하지만 loc는 index가 정수형이 아닌경우(특정값 ex) 20130102 )인 경우를 고려해주어야 한다


```python
# df.loc[3]        # index가 3인 row의 값들을 선택
# df.loc[0:3]      # index 0~2 슬라이싱
# df.loc[[0,3]]
```


```python
# df.age >300  # 블리언 타입 출력
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



> boolean값 활용 indexing <br>


```python
def re_index(df):
    return df.age > 300  # age 300 이상 블리언 판별 함수

df.loc[re_index(df)]  #  loc의 행을 함수값으로 줌  
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



> 함수 활용 <br>


```python
# df.loc[:,['cid','age','job']]  #  loc [행 전체 , 컬럼 사용자지정]

df.loc[35:45,['age','cid']]  # loc [35~45 행, 컬럼 사용자 지정]
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
      <th>age</th>
      <th>cid</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>35</th>
      <td>59</td>
      <td>C00109</td>
    </tr>
    <tr>
      <th>36</th>
      <td>45</td>
      <td>C00110</td>
    </tr>
    <tr>
      <th>37</th>
      <td>29</td>
      <td>C00111</td>
    </tr>
    <tr>
      <th>38</th>
      <td>46</td>
      <td>C00112</td>
    </tr>
    <tr>
      <th>39</th>
      <td>36</td>
      <td>C00114</td>
    </tr>
    <tr>
      <th>40</th>
      <td>57</td>
      <td>C00120</td>
    </tr>
    <tr>
      <th>41</th>
      <td>29</td>
      <td>C00127</td>
    </tr>
    <tr>
      <th>42</th>
      <td>31</td>
      <td>C00129</td>
    </tr>
    <tr>
      <th>43</th>
      <td>38</td>
      <td>C00133</td>
    </tr>
    <tr>
      <th>44</th>
      <td>43</td>
      <td>C00138</td>
    </tr>
    <tr>
      <th>45</th>
      <td>46</td>
      <td>C00140</td>
    </tr>
  </tbody>
</table>
</div>



<br>


```python
df.iloc[0:10,1]   # iloc 사용
```




    0    47
    1    33
    2    58
    3    28
    4    40
    5    44
    6    39
    7    46
    8    57
    9    51
    Name: age, dtype: int64



> iloc <br>
> iloc는 loc와 다르게 integer 타입으로만 범위 지정이 가능하다 <br>
> loc처럼 특정 값의 형식으로 index를 지정할 수 없고 오직 몇번째인지 integer형식으로만 지정 가능
> df.iloc[row index range , column range]
<br><br>

### 3. Data Setting
<br><br>


```python
# 데이터 프레임에 새로운 col을 추가할 경우 index range에 맞게 값 지정해주는 방법

df_2 = df # 복사본 생성
# df_2['E'] = df['cid']  # df_2[E] 컬럼을 원본읜 cid컬럼 가져와서 생성 (* 행범위 맞추기 위해)
# 이런식으로 만들면 이미 만들어져 있는(범위에 맞게) 컬럼만 사용가능


df_2.loc[:,'E'] = np.array([5] * len(df_2))  # df_2의 E컬럼선택후 np.array로 df_2의 len만큼 5 지정
df_2.loc[0:10,['E']]  ## 확인
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
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>5</td>
    </tr>
    <tr>
      <th>7</th>
      <td>5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>5</td>
    </tr>
    <tr>
      <th>9</th>
      <td>5</td>
    </tr>
    <tr>
      <th>10</th>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
#  df2 = df.copy()
#  df2[df2 > 0] = -df2  
#  df2
```

<br><br>
###  4. Missing Data(결측치)
<br>

> 결측값 확인하기
<br>


```python
# df.isnull() # 실행시 전체 dataset 결측값 여부 true / false 형식으로 반환    # notnull 은 반대로 반환
```


```python
df.isnull().sum()  # 컬럼별 결측값 개수 확인

# df.notnull().sum()  # 컬럼별 결측값을 제외한 값의 개수 확인
```




    cid            0
    age            0
    job           87
    marital        0
    education    568
    default        0
    balance        0
    housing        0
    loan           0
    dtype: int64




```python
df['education'].isnull().sum()   # 특정컬럼 결측값 개수 확인
```




    568




```python
df.isnull().sum(1)  # row 별 결측값 개수 확인

# df.notnull().sum(1)  # row 별 결측값 제외 개수 확인
```

<br>
> 결측값 처리하기


```python
df.isnull().sum()
```




    cid            0
    age            0
    job           87
    marital        0
    education    568
    default        0
    balance        0
    housing        0
    loan           0
    dtype: int64




```python
# df_3 = df  #  복사본 생성
# df_3.fillna(value=5)  # 모든 결측값을 5로 대체
# df_3.filna(value="string")  # 모든 결측값을 missing라는 str값으로 대체

# df_4 = df
# df_4.dropna(how='any')  # 결측값을 가지고 있는 모든 행 제거

# df_5 = df
# df_5.isna()   # 데이터프레임의 모든 값을 boolean 형태로 표시하고 결측값만 True값으로
```

> 결측값 연산시 <br>

1. sum, comsum 연산시 => 0으로 처리 <br>
2. mean, std 연산시 => 분석대상에서 제외 <br>
3. column간 연산시 하나라도 결측값이면 결측값으로 반환됨 ( ex) 컬럼1 + 컬럼2 = 컬럼3 으로 표현하는 경우) <br>
4. dataframe간 연산시 동일한 컬럼끼리는 non을 0으로 처리, 한쪽에만 존재하는 컬럼과의 연산은 non 반환
<br><br>

#### apply로 함수 적용

<br>

> 인자를 여러개 받을 경우 => apply 사용


```python
df_5['age'].iloc[:10].apply(np.cumsum)   # np.cumsum함수를 apply 사용하여 적용
```




    0    [47]
    1    [33]
    2    [58]
    3    [28]
    4    [40]
    5    [44]
    6    [39]
    7    [46]
    8    [57]
    9    [51]
    Name: age, dtype: object




```python
df_t = pd.DataFrame({'A' : [1,2,3,4],
                    'C' : pd.Series(1,index=list(range(4)),dtype='float32') })

df_t # testDF 생성
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
      <th>A</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_t[['A','C']].apply(lambda x: x.max()-x.min(), axis = 0 )  # axis=0 =>  column 기준 함수연산
df_t[['A','C']].apply(lambda x: x.max()-x.min(), axis = 1 )  # axis=1 => row별 함수연산
```

<br>
##### lambda  

<br>

>'익명함수'를 뜻하며, 변수에 할당하지 않고 사용한다 <br>
> 함수를 간단하게 사용할 수 있음

<br>

* lambda 인자 : 표현식


```python
#  hap 함수정의
def hap(x, y):
    return x + y
```


```python
# hap함수를 lambda로
(lambda x,y: x + y)(10, 20)
```

<br>
#### map
<br>
> map(함수,리스트) <br>
> map은 함수와 리스트를 인자로 받은후, 리스트로부터 하나씩 값을 꺼내 함수를 적용시킨 후 새로운 리스트에 결과값을 담는다



```python
# 1. lambda 함수 생성
# lambda x : x**2

# 2. map 함수 생성 => map(함수,리스트)  ## range(5) => [0,1,2,3,4] 리스트 반환
map(lambda x:x**2,range(5))

# 3. map함수의 결과를 새로운 list에 담아냄
list(map(lambda x : x**2,range(5)))
```




    [0, 1, 4, 9, 16]



<br>
#### reduce
<br>
> reduce는 *순서형자료(리스트,튜플,문자열)의 원소들을 누적적으로 함수에 적용시켜 줌 <br>
> reduce(함수,순서형자료)


```python
# from functools import reduce  # reduce import

reduce(lambda x,y : x+y , range(5))
# reduce(lambda x,y : x+y , [0,1,2,3,4])
# reduce(lambda x,y : x+y , "안녕하세요")
# reduce(lambda x,y : x+y , (3,4,5))
```




    10



<br>
#### filter
<br>

> filter(함수,리스트) <br>
> 리스트에서 함수의 조건에 참인값들을 걸러 새로운 리스트에 담아냄 <br>


```python
list(filter(lambda x : x>5 ,range(10)))
```




    [6, 7, 8, 9]




```python
list(filter(lambda x : x, [-1,-2,0,1,2,3,4]))  # 0은 F값이므로 걸러짐 즉, 0이 되는것을 함수에 의해 0(Flase)가 되는것을 filterling
```




    [-1, -2, 1, 2, 3, 4]



<br><br>
###  5. GROUPING
<br><br>

<br>

> 몇몇 기준에 따라 여러 그룹으로 데이터를 분할 (splitting) <br>
> 각 그룹에 독립적으로 함수를 적용 (applying) <br>
> 결과물들을 하나의 데이터 구조로 결합 (combining) <br>
<br>

> 통계량을 계산할 열.groupby(기준 열)
> 지정한 "그룹"별로 통계량 측정 위해 사용


```python
## job 기준 groupby
df_grouped_job = df.groupby(df['job']).max()
df_grouped_job
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
      <th>marital</th>
      <th>education</th>
      <th>default</th>
      <th>balance</th>
      <th>housing</th>
      <th>loan</th>
    </tr>
    <tr>
      <th>job</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>admin.</th>
      <td>C45174</td>
      <td>69</td>
      <td>single</td>
      <td>3.0</td>
      <td>yes</td>
      <td>18188</td>
      <td>yes</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>blue-collar</th>
      <td>C45182</td>
      <td>70</td>
      <td>single</td>
      <td>3.0</td>
      <td>yes</td>
      <td>66653</td>
      <td>yes</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>entrepreneur</th>
      <td>C45176</td>
      <td>270</td>
      <td>single</td>
      <td>3.0</td>
      <td>yes</td>
      <td>42045</td>
      <td>yes</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>housemaid</th>
      <td>C45030</td>
      <td>82</td>
      <td>single</td>
      <td>3.0</td>
      <td>yes</td>
      <td>23663</td>
      <td>yes</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>management</th>
      <td>C45198</td>
      <td>380</td>
      <td>single</td>
      <td>3.0</td>
      <td>yes</td>
      <td>98417</td>
      <td>yes</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>retired</th>
      <td>C45205</td>
      <td>92</td>
      <td>single</td>
      <td>3.0</td>
      <td>yes</td>
      <td>81204</td>
      <td>yes</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>self-employed</th>
      <td>C45098</td>
      <td>71</td>
      <td>single</td>
      <td>3.0</td>
      <td>yes</td>
      <td>34247</td>
      <td>yes</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>services</th>
      <td>C45186</td>
      <td>69</td>
      <td>single</td>
      <td>3.0</td>
      <td>yes</td>
      <td>57435</td>
      <td>yes</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>student</th>
      <td>C45204</td>
      <td>47</td>
      <td>single</td>
      <td>3.0</td>
      <td>yes</td>
      <td>24025</td>
      <td>yes</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>technician</th>
      <td>C45183</td>
      <td>71</td>
      <td>single</td>
      <td>3.0</td>
      <td>yes</td>
      <td>29207</td>
      <td>yes</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>unemployed</th>
      <td>C45167</td>
      <td>65</td>
      <td>single</td>
      <td>3.0</td>
      <td>yes</td>
      <td>19690</td>
      <td>yes</td>
      <td>yes</td>
    </tr>
  </tbody>
</table>
</div>




```python
##  job컬럼 기준 balance 평균
df_grouped_job_balance = df['balance'].groupby(df['job']).mean()
df_grouped_job_balance
```




    job
    admin.            939.976760
    blue-collar      1071.583807
    entrepreneur     1363.362981
    housemaid        1330.928753
    management       1773.943856
    retired          2087.175595
    self-employed    1752.765864
    services         1013.221951
    student          1551.338762
    technician       1238.845514
    unemployed       1536.778920
    Name: balance, dtype: float64




```python
## job,marital(2개 컬럼) 기준 balance 평균
df_grouped_job_marital = df['balance'].groupby([df['job'],df['marital']]).mean()
df_grouped_job_marital
```




    job            marital
    admin.         divorced     758.852814
                   married     1019.399464
                   single       907.066163
    blue-collar    divorced     640.765766
                   married     1129.329787
                   single      1023.310744
    entrepreneur   divorced    1036.860000
                   married     1500.523810
                   single      1030.027778
    housemaid      divorced    1478.473684
                   married     1138.844828
                   single      2359.065217
    management     divorced    1577.430818
                   married     1870.109547
                   single      1666.394318
    retired        divorced    1896.000000
                   married     2153.207101
                   single      1821.615385
    self-employed  divorced    1706.800000
                   married     1846.223404
                   single      1571.162963
    services       divorced     920.386076
                   married     1176.556172
                   single       719.501425
    student        divorced    1092.333333
                   married     1062.066667
                   single      1581.498270
    technician     divorced     880.161172
                   married     1330.523539
                   single      1219.580769
    unemployed     divorced    1293.696970
                   married     1567.086364
                   single      1546.735294
    Name: balance, dtype: float64



<br><br>
### 6. Categorical Data
<br><br>


```python
# 범주형 data로 변환하기
df_category = pd.DataFrame({"id":[1,2,3,4,5,6], "raw_grade":['a', 'b', 'b', 'a', 'a', 'e']})
df_category
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
      <th>id</th>
      <th>raw_grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>a</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>b</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>b</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>a</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>a</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>e</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df_category.info()  # dataset 확인

# 카테고리형으로 변환
df_category['grade'] = df_category['raw_grade'].astype('category')
```


```python
## 카테고리 이름 변경
# Series.cat.categories
df_category['grade'].cat.categories = ["very good", "good", "very bad"]

df_category
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
      <th>id</th>
      <th>raw_grade</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>a</td>
      <td>very good</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>b</td>
      <td>good</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>b</td>
      <td>good</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>a</td>
      <td>very good</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>a</td>
      <td>very good</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>e</td>
      <td>very bad</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_category.groupby(df_category['grade']).size()
```




    grade
    very good    3
    good         2
    very bad     1
    dtype: int64
