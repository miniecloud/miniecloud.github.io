---
title: Dataframe 다루기
author: mini
date: 2022-12-12 10:20:00 +0800
categories: [Python, pandas]
tags: [dataframe]
math: true
toc : true
---

### 1. dataframe 생성
```python
import pandas as pd
df = pd.Dataframe(data, columns=columns)
```
<br/>
### 2. dataframe 변환
#### - csv to dataframe  
```
pd.read_csv('test.csv', seg=',', encoding='utf-8', header=0)
```
-  그 외 파라미터   
	usecols=['col1'] - 사용할 열 지정  
	na_filter = True - 결측값 포함할지 포함하지 않을지(bool)  
	names=['col1'] - 컬럼명 지정  

#### - dataframe to csv 
```
pd.to_csv('test.csv', encoding='utf-8', header=True, index=False)
```
#### - DB 테이블 dataframe으로 불러오기
```python
import pandas.io.sql as psql
psql.read_sql(sql, db)
```	
<br/>

### 3. dataframe 병합
#### - concat
```
pd.concat(['df1','df2'])
```
#### - merge
공통 컬럼을 기준으로 병합할때  
```
pd.merge(df1,df2, how='',on='id')
```
> ※ merge 방법  
 	outer : 키 합집합, sql outer조인과 유사  
	inner : (inner join)   
	left : 왼쪽 프레임 키 사용 (left outer join)  
	right : 오른쪽 프레임 키 사용 (right outer join)   
	cross : 데카르트곱   

<br/>	
### 4. 데이터 삽입
데이터들을 리스트로 정리하여 넣는 경우가 많아 위와같은 방법으로 데이터를 추가해준다. 
```
df.append(pd.Series(data, index=df.columns), ignore_index=True)
```
<br/>	
### 5. 데이터 변경
#### - 특정컬럼으로 정렬
```
df.sort_values(by=['id'])
```
#### - 컬럼명 변경
```
df.rename(columns={'name':'new_name'}, inplace = True)
```
#### - 값변경
```
df.replace({np.nan:None})
```
#### - 값의 특정 글자 변경
```
df['column'].str.replace(pat=r'', repl=r'', regex=True)
```
* pat : 찾을 정규식표현	  
repl : 대체값  
regex : True = 패턴이 정규식이라고 가정, False = 패털을 리터럴 문자열로 처리, None ...(defalut True)


#### - 칼럼 타입 변경 
```
df.astype({'column':'datetime64[ns]'})
```
#### - None 값이 포함된 열 타입 변경
```
df['test'] = pd.array(df['test'], dtype=pd.Int64Dtype())
```

#### - 칼럼 또는 데이터 값 변경
 1. 칼럼
```
df.rename(columns={'original_name':'changied_name'}, inplace=True)
```
 2. 데이터
```
df.replace({np.nan: None}, inplace=True)
```

<br/>
### 6. 기타  

#### - 중복값 처리
```
df.duplicated(['column1', 'column2'], keep='first')
```
* keep  
first : 중복값 첫번째 값만 False, 나머지 중복값 True 반환  
last : 중복값 마지막 값만 False, 처음부터 마지막 전까지는 True 반환   
False : 중복값 모두 True 반환
```
df.drop_duplicates(['column1'], keep='first')
```	
* keep : 남길값 지정
위의 keep 과 유사함

#### - 특정 열의 특정값 찾기
```
df[df['columns'].isin([None])==True]
```
#### - 모든 행(열)을 확인
```
pd.set_option('display.max_columns(rows)', None)
```
#### - 특정 두가지 열 딕셔너리 형태로 변경
```
pd.Series(df['columns_values'].values, index=df['columns_key']).to_dict()
```

#### - 특정 두가지 열 column과 value로 df형 변환
```
pd.Series(df['columns_value'].values, index=df['columns_key'].to_frame().T)
```

#### - concat(axis=1)할때 행이 달라질때
concat할 데이터프레임의 index를 없애주면 된다. 
```
df1.reset_index(drop=True, inplace=True)
df2.reset_index(drop=True, inplace=True)
df = pd.concat([df1, df2], axis=1)
```

