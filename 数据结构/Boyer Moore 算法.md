---
title: Boyer Moore 算法
categories: 数据结构
aliases:
  - BM算法
---
# Boyer Moore 算法
## 基本概念
**Boyer Moore 算法（BM 算法）**：由 Robert S. Boyer 和 J Strother Moore 于 1977 年提出，是一种高效的字符串搜索算法，实际应用中通常比 KMP 算法快 3~5 倍。
- **BM 算法核心思想**：先对模式串 p 预处理，生成辅助表。在匹配过程中，如果文本串T某字符与模式串p不匹配，通过启发式规则，直接跳过不可能匹配的位置，将模式串整体向后滑动多位。
## 算法步骤
1. 计算文本串T的长度n和模式串p的长度m。
2. 对模式串p进行预处理，分别生成坏字符表bc_table和好后缀规则后移位数表 gs_table。
3. 将模式串p的头部与文本串T的当前位置i对齐，初始i=0。每次从模式串的末尾（j=m−1）开始向前逐位比较：
    - 如果 $T[i+j]与 p[j]$相等，则继续向前比较下一个字符。
        - 如果模式串所有字符均匹配，则返回当前匹配的起始位置 ii。
    - 如果 $T[i+j]与p[j]$ 不相等：
        - 分别根据坏字符表和好后缀表，计算坏字符移动距离bad_move和好后缀移动距离good_move。
        - 取两者的最大值作为本轮的实际移动距离，即 i+=max⁡(bad_move, good_move)，然后继续下一轮匹配。
4. 如果模式串移动到文本串末尾仍未找到匹配，则返回−1。
## 内部实现：
```python
def boyerMoore(T: str, p: str) -> int:
    n, m = len(T), len(p)
    if m == 0:
        return 0
    btable = generate_btable(p)
    gtable = generate_gtable(p)
    i = 0
    while i <= n - m:
        j = m - 1
        while j >= 0 and T[i + j] == p[j]:
            j -= 1
        if j < 0:
            return i
        b_move = j - btable.get(T[i + j], -1)
        g_move = gtable[j]  
        i += max(b_move, g_move)
    return -1
def generate_btable(p: str):
    b_table = {}
    for i, ch in enumerate(p):
        b_table[ch] = i
    return b_table
def generate_gtable(p: str):
    m = len(p)
    gtable = [m for _ in range(m)]
    suffix = generatesuffix(p)
    j = 0
    for i in range(m - 1, -1, -1):
        if suffix[i] == i + 1:
            while j < m - 1 - i:
                if gtable[j] == m:
                    gtable[j] = m - 1 - i
                j += 1
    for i in range(m - 1):
        gtable[m - 1 - suffix[i]] = m - 1 - i
    return gtable
def generatesuffix(p: str):
    m = len(p)
    suffix = [m for _ in range(m)]
    suffix[m - 1] = m
    for i in range(m - 2, -1, -1):
        j = i
        while j >= 0 and p[j] == p[m - 1 - i + j]:
            j -= 1
        suffix[i] = i - j
    return suffix
```
## 复杂度分析：
| 指标       | 复杂度                 | 说明                                                  |
| -------- | ------------------- | --------------------------------------------------- |
| 最好时间复杂度  | O(n/m)              | 每次匹配时，模式串 pp 中不存在与文本串T中第一个匹配的字符，滑动距离最大，比较次数最少。      |
| 最坏时间复杂度  | O(m×n)              | 文本串T中有大量重复字符，且模式串 p由 m−1 个相同字符和一个不同字符组成，导致每次只能滑动一位。 |
| 平均时间复杂度  | 介于 O(n/m)与 O(m×n)之间 | 实际应用中通常远优于最坏情况，接近最好情况。                              |
| 预处理时间复杂度 | O(m+σ)              | 生成坏字符表和好后缀表，σ 为字符集大小。                               |
| 空间复杂度    | O(m+σ)              | 需存储坏字符表（σ）和好后缀表（m）。                                 |

- 其中n为文本串长度，m为模式串长度，σ为字符集大小。
- 当模式串p是非周期性的，在最坏情况下，BM 算法最多需要进行3n 次字符比较操作
Boyer-Moore（BM）算法通过坏字符规则和好后缀规则两种启发式策略，实现模式串的高效跳跃移动，是实际应用中性能最优的单模式串匹配算法之一。

- **优点**：
    - **实际性能优异**：在大多数实际应用中，BM 算法通常比 KMP 算法快 3~5 倍
    - **跳跃能力强**：通过坏字符和好后缀规则，能够跳过大量不可能匹配的位置
    - **从右到左比较**：充分利用模式串信息，减少不必要的字符比较
    - **启发式策略**：两种规则互补，最大化跳跃距离
- **缺点**：
    - **实现复杂**：特别是好后缀规则的预处理部分，理解和实现难度较高
    - **最坏情况退化**：在特定输入下可能退化到O(m×n)复杂度
    - **空间开销**：需要存储坏字符表和好后缀表，空间复杂度为O(m+σ)
    - **预处理开销**：需要预先构建两个辅助表，不适合单次匹配场景
## 应用场景：
- 28.[找出字符串中第一个匹配项的下标](找出字符串中第一个匹配项的下标.md)