---
title: 子数组最大平均数I-LeetCode
categories: 作业练习
tags:
  - LeetCode
数据结构:
  - 数组滑动窗口
  - 固定长度滑动窗口
date: 2026-03-17
---
# 子数组最大平均数I

## 🎯 问题描述（来源于LeetCode）
**描述**：
给你一个由 `n` 个元素组成的整数数组 `nums` 和一个整数 `k` 。
请你找出平均数最大且 **长度为 `k`** 的连续子数组，并输出该最大平均数。
任何误差小于 `10-5` 的答案都将被视为正确答案。
**说明**：
- `n == nums.length`
- `1 <= k <= n <= 105`
- `-104 <= nums[i] <= 104`

**示例**：

- 示例 1：

```text
输入：nums = [1,12,-5,-6,50,3], k = 4
输出：12.75
解释：最大平均数 (12-5-6+50)/4 = 51/4 = 12.75
```

- 示例 2：

```text
输入：nums = [5], k = 1
输出：5.00000
```
## 💻 解题思路
### 思路1：固定长度滑动窗口
#### 思路1：代码实现
```python
class Solution:
    def findMaxAverage(self, nums: List[int], k: int) -> float:
        left,right=0,0
        max_waa=float('-inf')
        waa=0
        while right < len(nums):
            waa+=nums[right]
            if right-left+1>=k:
                if waa>max_waa:
                    max_waa=waa
                waa-=nums[left]
                left+=1
            right+=1
        return max_waa/k
```
#### 思路1：📊 性能分析
##### 提交结果
- **运行时间**：111ms击败33.40%
- **内存消耗**：28.84MB击败27.58%
##### 复杂度验证
- 时间复杂度：$O(N)$
- 空间复杂度：$O(1)$
#### 思考
