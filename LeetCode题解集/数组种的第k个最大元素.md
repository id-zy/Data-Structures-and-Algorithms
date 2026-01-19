---
title: 数组种的第k个最大元素-LeetCode
categories: 作业练习
tags:
  - LeetCode
数据结构:
  - 堆
  - 堆排序
  - 分治
date: 2026-01-19
---
# 数组种的第k个最大元素

## 🎯 问题描述（来源于LeetCode）
**描述**：
给定整数数组 `nums` 和整数 `k`，请返回数组中第 **k**个最大的元素。

请注意，你需要找的是数组排序后的第 `k` 个最大的元素，而不是第 `k` 个不同的元素。

你必须设计并实现时间复杂度为 `O(n)` 的算法解决此问题。
**说明**：

- `1 <= k <= nums.length <= 105`
- `-104 <= nums[i] <= 104`

**示例**：

- 示例 1：

```text
输入: [3,2,1,5,6,4], k = 2
输出: 5
```

- 示例 2：

```text
输入:[3,2,3,1,2,4,5,5,6],k = 4
输出: 4
```
## 💻 解题思路
### 思路1：堆排序
#### 思路1：代码实现
```python
class Solution:
    def maxHeap(self,nums:[int],i:int,heap_size:int):
        while 1:
            l_i=2*i+1
            r_i=2*i+2
            lst=i
            if l_i<heap_size and nums[l_i]>nums[lst]:
                lst=l_i
            if r_i<heap_size and nums[r_i]>nums[lst]:
                lst=r_i
            if lst==i:
                break
            nums[i],nums[lst]=nums[lst],nums[i]
            i=lst
    def buildmaxHeap(self,nums:[int],heap_size:int)->None:
        for i in range (heap_size//2-1,-1,-1):
            self.maxHeap(nums,i,heap_size)
    def findKthLargest(self, nums: List[int], k: int) -> int:
        n=len(nums)
        heap_size=n
        self.buildmaxHeap(nums,heap_size)
        for i in range(1,k):
            nums[0],nums[n-i]=nums[n-i],nums[0]
            heap_size-=1
            self.maxHeap(nums,0,heap_size)
        return nums[0]
```
#### 思路1：📊 性能分析
##### 提交结果
- **运行时间**：423ms击败10.94%
- **内存消耗**：30.50MB击败17.30%
##### 复杂度验证
- 时间复杂度：$O(Nlogn)$
- 空间复杂度：$O(1)$
#### 思考
