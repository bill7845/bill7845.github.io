---
layout: post
title: 쥬피터 노트북
comments: true
categories: [Development Environment/Java]
tags: [Java]
---

# Project Name is encore mentoring school project

#### Overview
* 주어진 두가지의 Data set중 한가지를 선택하여 유의미한 분석결과를 도출하는 과정
* pandas 활용 데이터 전처리 위주 서술


#### Skill Set
* python(pandas) , R , Excel


#### Project Roll : Dataset을 전체적으로 어떤 방향으로 분석해 나갈것인가에 대한 분석 방법 설정  
* 팀내 유일한 python(pandas) 활용 가능자로서 팀원의 요구 및 설정된 방향에 맞추어 data 처리     


```python
import pandas as pd
import numpy as np

ds = pd.read_csv('cup98LRN.txt')
```

    C:\Anaconda3\lib\site-packages\IPython\core\interactiveshell.py:2785: DtypeWarning: Columns (8) have mixed types. Specify dtype option on import or set low_memory=False.
      interactivity=interactivity, compiler=compiler, result=result)



```python
ds.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 95412 entries, 0 to 95411
    Columns: 481 entries, ODATEDW to GEOCODE2
    dtypes: float64(97), int64(310), object(74)
    memory usage: 350.1+ MB


* 481개의 column과 95412개의 행 확인  
* 418개의 colum중 분석 방향에 맞는 colum을 추출하였으며 이는,   

  1. 기부 데이터를 활용한 기부액 증대 방안 마련  
    A. 기부액수별 상위권과 하위권을 구분한뒤 두 집단의 특성,차이 파악  
    B. 해당 과정을 위한 기부액수별 Grouping 과정  
    C. 1차적으로 인구통계적 기준에 근거하여 Column 추출  

* DATA Dictionary   
RAMNTALL - Lifetime 기부총액    
STATE - 거주지역   
AGE - 나이    
GENDER - 성별    
POP902 - 가족 수  
INCOME - 소득    
NUMPROM - Lifetime 프로모션 받은 횟수


```python
ds_f=ds[['RAMNTALL','STATE','AGE','GENDER','POP902','INCOME','NUMPROM']]
```

* RAMNT변수의 경우 lifte time 기부 총액을 나타내는 변수로, 해당 변수를 활용하여 기부액수 상,하위권 구분 과정을 거침  
* 해당 결과에 따라 130$ 이상을 'Major'변수로 할당(MAJOR=Y ,NONMAJOR=N)
* 'RAMNTALL','GENDER'변수의 Type을 category형으로 변경
* 결측값 파악 후 제거(결측값의 크기,전체 data에 미치는 영향을 파악 후 결정)


```python
def major_func(row):
    if row['RAMNTALL'] >= 130:
        return 'Y'
    else:
        return 'N'
```


```python
ds_f['RAMNTALL']=ds_f.apply(major_func,axis=1)
```

    C:\Anaconda3\lib\site-packages\ipykernel_launcher.py:1: SettingWithCopyWarning:
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      """Entry point for launching an IPython kernel.


* major_func 함수를 이용하여 major / nonmajor 구분
* apply 이용하여 적용


```python
ds_f=ds_f.rename(columns={'RAMNTALL':'MAJOR'})
ds_f['MAJOR'].astype('category')
ds_f['GENDER'].astype('category')
ds_f['STATE'].astype('category')
ds_f['TOTAL']=ds['RAMNTALL']
```


```python
#결측치 확인
ds_f.isnull().sum()
```




    MAJOR          0
    STATE          0
    AGE        23665
    GENDER         0
    POP902         0
    INCOME     21286
    NUMPROM        0
    TOTAL          0
    dtype: int64




```python
# 결측값 제거 , 1차 저장
ds_f=ds_f.dropna()
ds_f.to_pickle('feature_a')
```


```python
## MAJOR,NONMAJOR 분리 , 2차 저장(Y,N 별로)
ds_f_major = ds_f[ds_f['MAJOR']=='Y']
ds_f_nmajor = ds_f[ds_f['MAJOR']=='N']

ds_f_major.to_pickle('f_by_major')
ds_f_major.to_pickle('f_by_nmajor')
```

* major 분리 작업 후 State 집단간의 특징 파악위한 작업 진행
* STATE별 기부 총액을 파악하기 위한 변수 'TOTAL' 추가('RAMNTALL'변수 사용) # 순서상 위로 추가
* 이상치 여부 확인


```python
ds_f_major.groupby('STATE')['TOTAL'].mean().sort_values(ascending=False)
```




    STATE
    VA    353.600000
    WV    263.500000
    HI    251.405294
    NV    249.678613
    CA    234.339525
    ID    231.232826
    OR    228.707429
    AZ    228.300633
    MI    227.646137
    IL    227.023168
    CO    227.017222
    FL    226.529786
    TN    225.538059
    NC    224.511250
    PA    223.500000
    TX    223.104473
    MT    222.847701
    GA    222.474376
    MS    222.298269
    WY    221.812500
    AE    221.000000
    AL    219.943702
    WA    219.891329
    AR    219.752092
    IA    219.699763
    KS    218.205385
    MO    218.204323
    OK    216.932292
    WI    215.621818
    NH    215.353333
    NE    214.938222
    SC    214.220444
    NM    213.705524
    UT    212.180000
    NJ    212.000000
    IN    210.845882
    NY    208.833333
    RI    208.500000
    LA    205.810000
    KY    205.020147
    MN    204.360070
    MD    196.438571
    AK    196.384615
    ND    195.595238
    VT    188.000000
    ME    176.000000
    SD    175.574074
    MA    162.000000
    OH    153.000000
    DE    151.000000
    Name: TOTAL, dtype: float64




```python
##이상치 확인 결과 10명이하 STATE 제거 필요성 ?? drop 써버리면?
ds_f_major = ds_f_major[ds_f_major.STATE != 'VT']
ds_f_major = ds_f_major[ds_f_major.STATE != 'DE']
ds_f_major = ds_f_major[ds_f_major.STATE != 'AE']
ds_f_major = ds_f_major[ds_f_major.STATE != 'WV']
ds_f_major = ds_f_major[ds_f_major.STATE != 'NJ']
ds_f_major = ds_f_major[ds_f_major.STATE != 'MA']
ds_f_major = ds_f_major[ds_f_major.STATE != 'RI']
ds_f_major = ds_f_major[ds_f_major.STATE != 'NH']
ds_f_major = ds_f_major[ds_f_major.STATE != 'ME']
ds_f_major = ds_f_major[ds_f_major.STATE != 'OH']
ds_f_major = ds_f_major[ds_f_major.STATE != 'VA']
ds_f_major = ds_f_major[ds_f_major.STATE != 'NY']
ds_f_major = ds_f_major[ds_f_major.STATE != 'MD']
ds_f_major = ds_f_major[ds_f_major.STATE != 'PA']
```


```python
##이상치 재확인
ds_f_major.groupby('STATE')['MAJOR'].count().sort_values(ascending=True)
```




    STATE
    AK      26
    SD      27
    HI      34
    WY      40
    ND      42
    UT      75
    MT      87
    ID      92
    NM     105
    NE     135
    NV     137
    AR     153
    MS     156
    KS     208
    AL     235
    OK     253
    IA     253
    KY     273
    LA     284
    SC     293
    CO     360
    TN     371
    OR     389
    IN     408
    MN     430
    GA     441
    AZ     474
    MO     502
    WI     517
    WA     617
    NC     712
    MI    1152
    IL    1228
    TX    1357
    FL    1498
    CA    3011
    Name: MAJOR, dtype: int64




```python
## 이상치 제거 후 STATE별 TOTAL 평균치 확인
ds_f_major.groupby('STATE')['TOTAL'].mean().sort_values(ascending=False)
```




    STATE
    HI    251.405294
    NV    249.678613
    CA    234.339525
    ID    231.232826
    OR    228.707429
    AZ    228.300633
    MI    227.646137
    IL    227.023168
    CO    227.017222
    FL    226.529786
    TN    225.538059
    NC    224.511250
    TX    223.104473
    MT    222.847701
    GA    222.474376
    MS    222.298269
    WY    221.812500
    AL    219.943702
    WA    219.891329
    AR    219.752092
    IA    219.699763
    KS    218.205385
    MO    218.204323
    OK    216.932292
    WI    215.621818
    NE    214.938222
    SC    214.220444
    NM    213.705524
    UT    212.180000
    IN    210.845882
    LA    205.810000
    KY    205.020147
    MN    204.360070
    AK    196.384615
    ND    195.595238
    SD    175.574074
    Name: TOTAL, dtype: float64



* 같은 과정으로 NON_MAJOR도 진행


```python
##이상치 확인
ds_f_nmajor.groupby('STATE')['MAJOR'].count().sort_values(ascending=True)
```




    STATE
    AA       1
    WV       1
    DE       1
    RI       2
    VT       3
    NH       3
    ME       4
    AE       7
    MA       8
    AP       8
    CT       9
    NJ      10
    PA      11
    MD      13
    VA      21
    NY      22
    OH      28
    WY     111
    SD     118
    AK     134
    ND     138
    HI     216
    MT     231
    ID     269
    UT     274
    NE     327
    AR     366
    NM     368
    NV     436
    KS     566
    MS     567
    IA     642
    OK     670
    AL     763
    KY     863
    LA     894
    OR     912
    SC     922
    AZ    1107
    CO    1131
    MN    1143
    TN    1264
    IN    1415
    MO    1430
    GA    1554
    WI    1588
    WA    1621
    NC    2058
    MI    3201
    IL    3404
    TX    4188
    FL    4340
    CA    7635
    Name: MAJOR, dtype: int64




```python
#이상치 제거
ds_f_nmajor = ds_f_nmajor[ds_f_nmajor.STATE != 'AA']
ds_f_nmajor = ds_f_nmajor[ds_f_nmajor.STATE != 'WV']
ds_f_nmajor = ds_f_nmajor[ds_f_nmajor.STATE != 'DE']
ds_f_nmajor = ds_f_nmajor[ds_f_nmajor.STATE != 'RI']
ds_f_nmajor = ds_f_nmajor[ds_f_nmajor.STATE != 'VT']
ds_f_nmajor = ds_f_nmajor[ds_f_nmajor.STATE != 'NH']
ds_f_nmajor = ds_f_nmajor[ds_f_nmajor.STATE != 'ME']
ds_f_nmajor = ds_f_nmajor[ds_f_nmajor.STATE != 'AE']
ds_f_nmajor = ds_f_nmajor[ds_f_nmajor.STATE != 'MA']
ds_f_nmajor = ds_f_nmajor[ds_f_nmajor.STATE != 'AP']
ds_f_nmajor = ds_f_nmajor[ds_f_nmajor.STATE != 'CT']
```


```python
# 이상치 제거 후 STATE별 TOTAL 평균치 확인
ds_f_nmajor.groupby('STATE')['TOTAL'].mean().sort_values(ascending=False)
```




    STATE
    AA    124.000000
    NH    110.666667
    PA     77.454545
    WV     73.000000
    DE     71.000000
    AE     70.571429
    VA     70.047619
    SD     69.635763
    NJ     67.700000
    IA     67.519283
    MN     65.499379
    ND     65.393768
    KS     65.086590
    MT     64.913636
    KY     64.890197
    WI     64.712601
    OR     64.384167
    NE     64.221927
    AR     64.214617
    WA     64.147785
    MO     63.907734
    IL     63.481011
    FL     63.000724
    NC     62.845748
    IN     62.573251
    CO     62.540318
    MI     62.279300
    LA     62.214329
    CA     62.177679
    SC     62.006312
    NM     61.794538
    MS     61.544004
    UT     61.324124
    ID     61.134758
    MD     61.000000
    AL     60.855387
    OK     60.744776
    TX     60.672677
    WY     60.441441
    AZ     60.415827
    TN     60.334478
    GA     59.220991
    NY     59.136364
    CT     57.333333
    MA     57.250000
    NV     56.237546
    HI     54.087963
    AK     52.231343
    ME     48.500000
    OH     47.464286
    AP     44.500000
    VT     32.333333
    RI     23.500000
    Name: TOTAL, dtype: float64



* MAJOR , NONMAJOR 의 주별 기부총액 분리 결과    


* MAJOR의 경우 상위권 3개주 HI 251.405294   NV 249.678613   CA 234.339525   // 하위권 3개주 AK 196.384615   ND 195.595238   SD 175.574074


* NON_MAJOR의 경우 상위권 3개주 AA 124.000000  NH 110.666667  PA 77.454545   // 하위권 3개주 AP 44.500000   VT 32.333333   RI 23.500000


```python
def aa(row):
    for i in range(len(ds_f_nmajor)):
        if ['STATE'] == 'AA':
            return ds_f_nmajor = ds_f_nmajor[ds_f_nmajor.STATE != 'AA']

```


```python
ds_f_nmajor['STATE'].apply(aa)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-19-10f5d8e586ec> in <module>()
    ----> 1 ds_f_nmajor['STATE'].apply(aa)


    C:\Anaconda3\lib\site-packages\pandas\core\series.py in apply(self, func, convert_dtype, args, **kwds)
       3190             else:
       3191                 values = self.astype(object).values
    -> 3192                 mapped = lib.map_infer(values, f, convert=convert_dtype)
       3193
       3194         if len(mapped) and isinstance(mapped[0], Series):


    pandas/_libs/src\inference.pyx in pandas._libs.lib.map_infer()


    TypeError: aa() takes 0 positional arguments but 1 was given



```python
def major_func(row):
    if row['RAMNTALL'] >= 130:
        return 'Y'
    else:
        return 'N'
```
