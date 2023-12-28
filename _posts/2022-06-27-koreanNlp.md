---
title: 한국어 전처리
author: mini
date: 2022-06-27 11:50:00 +0800
categories: [Etc]
tags: [NLP]
toc : true
---

## 한국어 전처리
### PyKoSpacing
`pip install git+https://github.com/haven-jeon/PyKoSpacing.git`
```
from psykospacing import Spacing
spacing = Spacing()
kospacing_sent = spacing(new_sent)
```

### Py-Hanspell
네이버 한글 맞춤법 검사기를 바탕으로 만들어진 패키지

### Soynlp
품사 태깅, 단어 토큰화등을 지원하는 단어 토크나이저이다. 비지도 학습으로 단어 토큰화를 하며, 데이터에 자주 등장하는 단어들을 단어로 분석한다. 신조어 문제에 좋다.
또한 반본되는 문자 정제도 가능하다.

##### Customized KoNLPy
영어권 언어는 띄어쓰기만으로도 단어들이 잘 분리되지만 교착어인 한국어 특성상 문장에서 단어 추출이 제대로 되지 않을때가 많다. 그럴때, 형태소 분석기 Twitter에 add_dictionary('단어', '품사')를 사용하면 사전추가를 해줄 수 있다. 단어가 많으면 굉장히 번거로울 것 같다..ㅎ


※ 참고 자료
[한국어 전처리 패키지](https://wikidocs.net/92961)


## 토큰화
주어진 텍스트를 단어 또는 문자 단위로 자름

## 벡터화 Vectorization
자연어를 컴퓨터가 이해할 수 있도록 수치로 바꾸는 것

