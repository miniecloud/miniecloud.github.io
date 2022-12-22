---
title: dataframe 순회하기(데이터전처리)
author: mini
date: 2022-12-12 10:10:00 +0800
categories: [Python, pandas]
tags: [dataframe]
math: true
toc : true
---

 자연어 처리(NLP)를 하다보면 전처리해야할 일이 많다. 전처리를 할 때 dataframe 형식으로 데이터를 처리하는데 데이터의 양이 너무 많다보니 단순 for문은 속도 측면에서 매우 비효율적이다. 엄청 느리다.

## df.itterows()
`for index, data in df.iterrows()`

※ 진행상황 출력하기
```
import tqdm
for index, data in tqdm(df.iterrows(), total=df.shape[0])
```

## apply 
```
def test(x) : 
	pass
# 특정열 적용
df['column'] = df['column'].apply(lambda x: test(x))

# 여러 열 사용
df['column'] = df.apply(lambda row : test(row['column1'],row['column2']), axis=1)
```

