---
title: zip파일 압축해제 & 한국어 파일명 인코딩
author: mini
date: 2022-12-20 10:10:00 +0800
categories: [Python, file]
tags : [python]
toc : true
---

## zip 파일 다운로드 받기  
```python
from urllib import request
url = 'htts://~~~~.zip'
download_file_name = './data/test.zip'
request.urlretrieve(url, file)
```

## zip 파일 압축해제 & 한국어 제목 인코딩

```python
import zipfile
with zipfile.Zipfile(file, 'r') as zf :
	zipInfo = zf.infolist()	
	for zfile in zipInfo : 
		zfile.filename = zfile.filename.encode('cp437').decode('cp949', 'ignore')
		zf.extract(zfile, './data')
```

🛑 cp437에서 cp949로 변경해줘야 파일 이름이 안깨진다. 

## 파일 한번에 삭제
### glob()
 - 파일들의 리스트를 뽑을 때 사용
 - 인자로 받은 패턴과 이름이 일치하는 모든 파일들을 반환

```python
import os
import glob
[os.remove(f) for f in glob.glob('./data/*')]
```

