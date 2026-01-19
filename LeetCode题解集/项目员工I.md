---
title: 项目员工I-LeetCode
categories: 作业练习
tags:
  - LeetCode
数据结构:
  - sql
date: 2025-12-09
---
# 项目员工I

## 🎯 问题描述（来源于LeetCode）
**描述**：
项目表 `Project`： 
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| project_id  | int     |
| employee_id | int     |
+-------------+---------+
主键为 (project_id, employee_id)。
employee_id 是员工表 `Employee` 表的外键。
这张表的每一行表示 employee_id 的员工正在 project_id 的项目上工作。
员工表 `Employee`：
+------------------+---------+
| Column Name      | Type    |
+------------------+---------+
| employee_id      | int     |
| name             | varchar |
| experience_years | int     |
+------------------+---------+
主键是 employee_id。数据保证 experience_years 非空。
这张表的每一行包含一个员工的信息。
**要求**：
请写一个 SQL 语句，查询每一个项目中员工的 **平均** 工作年限，**精确到小数点后两位**。
以 **任意** 顺序返回结果表。
**说明**：
## 💻 解题思路
### 思路1：模拟
#### 思路1：代码实现
```sql
# Write your MySQL query statement below
select p.project_id,round(sum(e.experience_years)/count(*),2)as average_years
from Project p
left join Employee e
on p.employee_id=e.employee_id
group by p.project_id
```
#### 思路1：📊 性能分析
##### 提交结果
- **运行时间**：1168ms击败5.73%
#### 思考
照着题目描述做即可