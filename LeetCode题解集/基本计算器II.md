---
title: 基本计算器II-LeetCode
categories: 作业练习
tags:
  - LeetCode
数据结构:
  - 栈
date: 2026-03-18
---
# 基本计算器II

## 🎯 问题描述（来源于LeetCode）
**描述**：
给你一个字符串表达式 `s` ，请你实现一个基本计算器来计算并返回它的值。

整数除法仅保留整数部分。

你可以假设给定的表达式总是有效的。所有中间结果将在 `[-231, 231 - 1]` 的范围内。

注意：不允许使用任何将字符串作为数学表达式计算的内置函数，比如 `eval()` 。
**说明**：
- `1 <= s.length <= 3 * 105`
- `s` 由整数和算符 `('+', '-', '*', '/')` 组成，中间由一些空格隔开
- `s` 表示一个 **有效表达式**
- 表达式中的所有整数都是非负整数，且在范围 `[0, 231 - 1]` 内
- 题目数据保证答案是一个 **32-bit 整数**
**示例**：

- 示例 1：

```text
输入：s = "3+2*2"
输出：7
```

- 示例 2：

```text
输入：s = " 3/2 "
输出：1
```
## 💻 解题思路
### 思路1：栈
#### 思路1：代码实现
```python
class Solution:
    def calculate(self, s: str) -> int:
        stack=[]
        num=0
        op='+'
        s+='+'
        for x in s:
            if x.isdigit():
                num=num*10+int(x)
            elif x==' ':
                continue
            else:
                if op=='+':
                    stack.append(num)
                elif op=='-':
                    stack.append(-num)
                elif op=='*':
                    stack.append(stack.pop()*num)
                elif op == '/':
                    stack.append(int(stack.pop()/num))
                op=x
                num=0
        return sum(stack)
```
#### 思路1：📊 性能分析
##### 提交结果
- **运行时间**：39ms击败98.53%
- **内存消耗**：22.21MB击败21.72%
##### 复杂度验证
- 时间复杂度：$O(N)$
- 空间复杂度：$O(N)$
#### 思考
