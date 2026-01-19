---
title: H指数-LeetCode
categories: 作业练习
tags:
  - LeetCode
数据结构:
  - 数组
date: 2025-12-07
---
# H指数

## 🎯 问题描述（来源于LeetCode）
给你一个整数数组 `citations` ，其中 `citations[i]` 表示研究者的第 `i` 篇论文被引用的次数。计算并返回该研究者的 **`h` 指数**。

根据维基百科上 h 指数的定义：`h` 代表“高引用次数” ，一名科研人员的 `h` **指数** 是指他（她）至少发表了 `h` 篇论文，并且 **至少** 有 `h` 篇论文被引用次数大于等于 `h` 。如果 `h` 有多种可能的值，**`h` 指数** 是其中最大的那个。
## 💻 代码实现
```python
class Solution:
    def hIndex(self, citations: List[int]) -> int:
        l=len(citations)
        nums=citations
        count=0
        acount=0
        h=0
        nums.sort()
        for i in range(l+1):
            x=i
            count =i
            for num in nums:
                if num >=i:
                    count-=1
            if count<=0:
                acount=i
                if x>acount:
                    acount=x
        return acount
```


## 📊 性能分析
### 提交结果
- **运行时间**：347ms击败  5.07%
- **内存消耗**：17.79MB击败53.59%
### 复杂度验证
- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$
## 优化算法：
```python
class Solution:
    def hIndex(self, citations: List[int]) -> int:
        l=len(citations)
        nums=citations
        nums.sort()
        for i,num in enumerate(nums):
            if l-i<=num:
                return l-i
        return 0
```
### 复杂度验证
- 时间复杂度：$O(nlog(n))$
- 空间复杂度：$O(n)$