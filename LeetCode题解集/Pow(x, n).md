---
title: Pow(x, n)
categories: 作业练习
tags:
  - LeetCode
数据结构:
  - 位运算
  - 快速幂
date: 2025-11-30
---
# Pow(x, n)

## 🎯 问题描述（来源于LeetCode）
```
实现pow(_x_, _n_) ，即计算x的整n次幂函数（即，x^n ）。
```
## 💻 代码实现
{% tabs pow算法 %}
<!-- tab  暴力破解 -->
```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
         ans=1.0
         i=0
         if n<0:
            x=1/x
            n=-n
         for i in range(n):
            ans*=x
         return ans
```

<!-- endtab -->
<!-- tab 快速幂优化算法 -->
使用[快速幂](快速幂.md)降低其时间复杂度
```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
         ans=1.0
         i=0
         if n<0:
            x=1/x
            n=-n
         while n:
            if(n&1==1):
                ans*=x
            x*=x
            n>>=1
         return ans
```

<!-- endtab -->
{% endtabs %}
## 📊 性能分析
### 提交结果
- **运行时间**：0ms击败100.00 %
- **内存消耗**：17.40MB击败 94.00%
### 复杂度验证
- 时间复杂度：$O(log(n))$
- 空间复杂度：$O(1)$
