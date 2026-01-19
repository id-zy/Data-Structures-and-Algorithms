---
title: Excel 表列名称
categories: 作业练习
tags:
  - LeetCode
数据结构:
  - 数学
date: 2025-12-02
---
# Excel 表列名称

## 🎯 问题描述（来源于LeetCode）
```TEXT
给你一个整数 columnNumber，返回它在 Excel 表中相对应的列名称。
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
    def convertToTitle(self, columnNumber: int) -> str:
        n=columnNumber
        s=''
        while (n > 0):
           m = n % 26
           if (m == 0): m = 26
           s = chr(m + 64) + s
           n = (n - m) // 26
        return s
```
## 📊 性能分析
### 提交结果
- **运行时间**：0ms击败100.00%
- **内存消耗**：17.38MB击败93.22%
### 复杂度验证
- 时间复杂度：$O(log(n))$
- 空间复杂度：$O(1)$
