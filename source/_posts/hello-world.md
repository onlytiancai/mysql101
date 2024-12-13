---
title: 001 MySQL 入门
---


MySQL是一种流行的开源数据库管理系统（DBMS），充分支持SQL。这篇博客将讲解MySQL的基础学习，并举例演示常见SQL语句。

---

## 1. 初始化MySQL数据库

### 连接数据库

在安装好MySQL后，通过命令行连接：
```bash
mysql -u root -p
```
输入密码，连接成功后，将看到MySQL控制台。

### 创建一个新数据库
使用 `CREATE DATABASE` 命令：
```sql
CREATE DATABASE demo_db;
```
查看存在的数据库：
```sql
SHOW DATABASES;
```

### 选择数据库
使用 `USE` 命令选择刚创建的数据库：
```sql
USE demo_db;
```

---

## 2. 表操作

### 创建表
使用 `CREATE TABLE` 命令创建表：
```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 查看表
查看存在的表：
```sql
SHOW TABLES;
```
查看表结构：
```sql
DESCRIBE users;
```

---

## 3. 数据操作

### 插入数据
使用 `INSERT INTO` 命令插入数据：
```sql
INSERT INTO users (name, email)
VALUES ('Alice', 'alice@example.com'),
       ('Bob', 'bob@example.com');
```

### 查询数据
基础查询：
```sql
SELECT * FROM users;
```
指定列查询：
```sql
SELECT name, email FROM users;
```
加入条件：
```sql
SELECT * FROM users WHERE name = 'Alice';
```

### 更新数据
使用 `UPDATE` 命令：
```sql
UPDATE users
SET email = 'alice.new@example.com'
WHERE name = 'Alice';
```

### 删除数据
使用 `DELETE` 命令：
```sql
DELETE FROM users WHERE name = 'Bob';
```

---

## 4. 进阶操作

### 排序
使用 `ORDER BY` 进行排序：
```sql
SELECT * FROM users ORDER BY created_at DESC;
```

### 分组
使用 `GROUP BY` 进行分组：
```sql
SELECT COUNT(*) AS user_count, created_at
FROM users
GROUP BY created_at;
```

### 连接表
使用 `JOIN` 连接两个表：
```sql
SELECT orders.id, users.name, orders.total_price
FROM orders
INNER JOIN users ON orders.user_id = users.id;
```

---

## 5. 优化常见问题

### 创建指定
通过创建指定优化查询速度：
```sql
CREATE INDEX idx_name ON users (name);
```

### 使用规范化表结构
确保表结构不重复，减少数据冲突。举例：将订单信息和用户信息分开。

---

通过上述示例，尤其是基本操作，将为你学习MySQL打下基础！
