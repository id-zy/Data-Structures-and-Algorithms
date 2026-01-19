---
title: 文章浏览I
categories: 作业练习
tags:
  - LeetCode
---
# 文章浏览I
## 题目描述（来源于LeetCode)
`Views` 表：

+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| article_id    | int     |
| author_id     | int     |
| viewer_id     | int     |
| view_date     | date    |
+---------------+---------+
此表可能会存在重复行。（换句话说，在 SQL 中这个表没有主键）
此表的每一行都表示某人在某天浏览了某位作者的某篇文章。
请注意，同一人的 author_id 和 viewer_id 是相同的。

请查询出所有浏览过自己文章的作者。

结果按照作者的 `id` 升序排列。

### 初期思路
```sql
# Write your MySQL query statement below
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id=viewer_id
ORDER BY author_id ASC
```




