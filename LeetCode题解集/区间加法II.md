---
title: 区间加法II-LeetCode
categories: 作业练习
tags:
  - LeetCode
数据结构:
  - 数组
date: 2025-12-09
---
# 区间加法II

## 🎯 问题描述（来源于LeetCode）
**描述**：
给你一个 `m x n` 的矩阵 `M` 和一个操作数组 `op` 。矩阵初始化时所有的单元格都为 `0` 。`ops[i] = [ai, bi]` 意味着当所有的 `0 <= x < ai` 和 `0 <= y < bi` 时， `M[x][y]` 应该加 1。
**要求**：
在 _执行完所有操作后_ ，计算并返回 _矩阵中最大整数的个数_ 。
**说明**：
- `1 <= m, n <= 4 * 104`
- `0 <= ops.length <= 104`
- `ops[i].length == 2`
- `1 <= ai <= m`
- `1 <= bi <= n`

**示例**：

- 示例 1：
**输入:** m = 3, n = 3，ops = [[2,2],[3,3]]
**输出:** 4
**解释:** M 中最大的整数是 2, 而且 M 中有4个值为2的元素。因此返回 4。

- 示例 2：

**输入:** m = 3, n = 3, ops = [[2,2],[3,3],[3,3],[3,3],[2,2],[3,3],[3,3],[3,3],[2,2],[3,3],[3,3],[3,3]]
**输出:** 4
## 💻 解题思路
### 思路1：模拟（暴力破解）
#### 思路1：代码实现
```python
class Solution:
    def maxCount(self, m: int, n: int, ops: List[List[int]]) -> int:
        M=[[0]*n for _ in range(m)]
        count=0
        for i in range(len(ops)):
            ai,bi=ops[i]
            for i,j in product(range(ai),range(bi)):
                M[i][j]+=1
        max1=0
        for i,j in product(range(m),range(n)):
            if M[i][j]>max1:
                max1=M[i][j]
        for i,j in product(range(m),range(n)):
            if M[i][j]==max1:
                count+=1
        return count
```
#### 思路1：📊 性能分析
##### 提交结果
- **运行时间**：
- **内存消耗**：超出内存限制
##### 复杂度验证
- 时间复杂度：$O(k × a × b + m × n)$，其中k是操作次数，a和b是每次操作的区域大小
- 空间复杂度：$O(m*n)$
#### 思考
当m,n很大时，二维数组占用空间过大，超出内存限制
### 思路2：思考重叠区域
#### 思路2：代码实现
```python
class Solution:
    def maxCount(self, m: int, n: int, ops: List[List[int]]) -> int:
        if len(ops)==0:
            return m*n
        a1,b1=ops[0]
        for i in range(len(ops)):
            ai,bi=ops[i]
            if a1>ai:
                a1=ai
            if b1>bi:
                b1=bi
        return a1*b1
```
#### 思路2：📊 性能分析
##### 提交结果
- **运行时间**：3ms击败34.41%
- **内存消耗**：18.87MB击败54.25%
##### 复杂度验证
- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$
#### 思考
只需要找到所有相加区域的重叠部分即可