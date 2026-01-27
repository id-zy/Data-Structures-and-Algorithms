---
title: 存在重复元素III-LeetCode
categories: 作业练习
tags:
  - LeetCode
数据结构:
  - 桶排序
  - 滑动窗口
date: 2026-01-27
---
# 存在重复元素III

## 🎯 问题描述（来源于LeetCode）
**描述**：
给你一个整数数组 `nums` 和两个整数 `indexDiff` 和 `valueDiff` 。
找出满足下述条件的下标对 `(i, j)`：

- `i != j`,
- `abs(i - j) <= indexDiff`
- `abs(nums[i] - nums[j]) <= valueDiff`
如果存在，返回 `true` _；_否则，返回 `false` 。
**说明**：
- `2 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`
- `1 <= indexDiff <= nums.length`
- `0 <= valueDiff <= 109`

**示例**：

- 示例 1：

```text
输入：nums = [1,2,3,1], indexDiff = 3, valueDiff = 0
输出：true
解释：可以找出 (i, j) = (0, 3) 。
满足下述 3 个条件：
i != j --> 0 != 3
abs(i - j) <= indexDiff --> abs(0 - 3) <= 3
abs(nums[i] - nums[j]) <= valueDiff --> abs(1 - 1) <= 0
```

- 示例 2：

```text
输入：nums = [1,5,9,1,5,9], indexDiff = 2, valueDiff = 3
输出：false
解释：尝试所有可能的下标对 (i, j) ，均无法满足这 3 个条件，因此返回 false 。
```
## 💻 解题思路
### 思路1：暴力破解
#### 思路1：代码实现
```PYTHON
class Solution:
    def containsNearbyAlmostDuplicate(
        self, nums: List[int], indexDiff: int, valueDiff: int) -> bool:
        for i in range(1, indexDiff + 1):
            r = 0
            l = r + i
            pid = False
            while l < len(nums):
                if abs(nums[l] - nums[r]) <= valueDiff:
                    pid = True
                    break
                r += 1
                l = r + i
            if pid:
                return pid
        return False
```
#### 思路1：📊 性能分析
##### 提交结果
- **运行时间**：超时
- **内存消耗**：
##### 复杂度验证
- 时间复杂度：$O(N \times \text{indexDiff})$，最坏可达 $O(N^2)$
- 空间复杂度：$O(1)$
#### 思考
暴力方法在数据规模较大时必然超时，因此不可行。
### 思路2：桶排序
#### 思路2：代码实现
```python
class Solution:
    def containsNearbyAlmostDuplicate(self, nums: List[int], indexDiff: int, valueDiff: int) -> bool:    
        bucket_size = valueDiff + 1
        buckets = {}
        for i, num in enumerate(nums):
            bucket_id = num // bucket_size  
            if bucket_id in buckets:
                return True
            if bucket_id - 1 in buckets and abs(num - buckets[bucket_id - 1]) <= valueDiff:
                return True
            if bucket_id + 1 in buckets and abs(num - buckets[bucket_id + 1]) <= valueDiff:
                return True
            buckets[bucket_id] = num
            if i >= indexDiff:
                old_bucket_id = nums[i - indexDiff] // bucket_size
                buckets.pop(old_bucket_id, None)
        return False
```
#### 思路2：📊 性能分析
##### 提交结果
- **运行时间**：143ms击败74.26%
- **内存消耗**：36.61MB击败10.05%
##### 复杂度验证
- 时间复杂度：$O(N)$
- 空间复杂度：$O(N)$
#### 思考
桶排序通过将值域分段，将差值判断转化为桶的查找，从而在 $O(1)$ 时间内完成相邻值的检查。  
滑动窗口确保索引差条件自然满足。