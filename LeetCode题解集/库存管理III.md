---
title: 库存管理III-LeetCode
categories: 作业练习
tags:
  - LeetCode
数据结构:
  - 堆
  - 堆排序
  - 分治
date: 2026-01-19
---
# 库存管理III

## 🎯 问题描述（来源于LeetCode）
**描述**：
仓库管理员以数组 `stock` 形式记录商品库存表，其中 `stock[i]` 表示对应商品库存余量。请返回库存余量最少的 `cnt` 个商品余量，返回 **顺序不限**。
**说明**：
- `0 <= cnt <= stock.length <= 10000`
- `0 <= stock[i] <= 10000`

**示例**：

- 示例 1：

```text
输入：stock = [2,5,7,4], cnt = 1
输出：[2]
```

- 示例 2：

```text
输入：stock = [0,2,3,6], cnt = 2
输出：[0,2] 或 [2,0]
```
## 💻 解题思路
### 思路1：最小堆排序
#### 思路1：代码实现
```python
class Solution:
    def maxHeap(self,nums:[int],i:int,heap_size:int):
        while 1:
            l_i=2*i+1
            r_i=2*i+2
            lst=i
            if l_i<heap_size and nums[l_i]<nums[lst]:
                lst=l_i
            if r_i<heap_size and nums[r_i]<nums[lst]:
                lst=r_i
            if lst==i:
                break
            nums[i],nums[lst]=nums[lst],nums[i]
            i=lst
    def buildmaxHeap(self,nums:[int],heap_size:int)->None:
        for i in range (heap_size//2-1,-1,-1):
            self.maxHeap(nums,i,heap_size)
    def inventoryManagement(self, stock: List[int], cnt: int) -> List[int]:
        if cnt == 0:
            return []
        n = len(stock)
        heap_size = min(cnt, n)
        self.buildmaxHeap(stock, n)
        result = []
        import copy
        temp = copy.deepcopy(stock)
        for i in range(min(cnt, n)):
            temp[0], temp[n - i - 1] = temp[n - i - 1], temp[0]
            result.append(temp[n - i - 1])
            self.maxHeap(temp, 0, n - i - 1)
        
        return result
```
#### 思路1：📊 性能分析
##### 提交结果
- **运行时间**：103ms击败18.65%
- **内存消耗**：20.32MB击败21.89%
##### 复杂度验证
- 时间复杂度：$O(Nlogn)$
- 空间复杂度：$O(1)$
#### 思考
