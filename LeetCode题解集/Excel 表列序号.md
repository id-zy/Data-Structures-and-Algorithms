---
title: Excel 表列序号
categories: 作业练习
tags:
  - LeetCode
数据结构:
  - 数学
date: 2025-12-02
---
#  Excel 表列序号

## 🎯 问题描述（来源于LeetCode）
```TEXT
给你一个字符串columnTitle，表示 Excel 表格中的列名称。返回 _该列名称对应的列序号_ 。
例如：
A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28 
...
```
## 💻 代码实现
```python
class Solution:
    def titleToNumber(self, columnTitle: str) -> int:
          s=columnTitle
          a = list(map(lambda x: chr(x), range(ord('A'), ord('Z') + 1)))
          l = len(s)
          sum = 0
          if l > 1:
              for i in range(l - 1):
                  index =a.index(s[i])
                  num = pow(26, l - 1) * (index + 1)
                  l = l - 1
                  sum = sum + num
              sum = sum+a.index(s[-1])
          else:
              sum = sum + a.index(s[-1])
```
## 📊 性能分析
### 提交结果
- **运行时间**：3ms击败20.74%
- **内存消耗**：17.43MB击败59.26%
### 复杂度验证
- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$
