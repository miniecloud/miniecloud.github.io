---
title: 데이터프레임 엑셀 특정 시트로 변경(openpyxl)
author: mini
date: 2022-12-20 10:10:00 +0800
categories: [Python, file]
tags: [dataframe]
toc : true
---

```python
import openpyxl
import openpyxl.utils.dataframe import dataframe_to_rows

wb = openpyxl.Workbook()

# sheet 추가
wb.crate_sheet('sheet_name', 1) # sheet 순서

# 데이터프레임 준비 
rows = dataframe_to_rows(df, index=False, header=True)

# 데이터프레임 -> excel sheet
for r_idx, row in enumerate(rows, 1):
	for c_idx, value in enumerate(row, 1):
		wb[sheet_name].cell(row=r_idx, column=c_idx, value=value)

wb.save('test.xlsx')
```
