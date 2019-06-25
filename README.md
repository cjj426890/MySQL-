# MySQL-
关于MySQL学习的一点点笔记
三大数据库（MySql、Redis、MongoDB）  

| 序号 |               软件程序               |
| :--: | :----------------------------------: |
|  1   | 了解关系型数据库的诞生原因和独特优势 |
|  2   |       安装并初始化MySQL数据库        |
|  3   |          学习管理MySQL服务           |
|  4   |        创建新用户，并分配权限        |
|  5   |        了解MySQL常用配置参数         |

### MySql数据库

```
+ 了解关系型数据库的重要性
    - 为什么会出现关系型数据库？
    - 有哪些常见的关系型数据库？
+ 掌握MySQL的安装和配置
    - 怎么安装MySQL数据库？
    - 怎么配置MySQL的字符集、端口号、IP地址绑定、数据目录等等
+ 实践用户创建、分配权限和密码找回
    - 如何创建root之外的账户并分配权限？
    - 忘记数据库密码，应该如何找回？
```

### 数据库简介  

- 操作系统中数据存放的载体
  - WIndows、Linux和MacOS都是基于文件的操作系统  
- 为什么要使用数据库管理数据？
  - 支持从海量数据中提取数据
  - Excel不支持关联信息的查找
- 什么是数据库系统？
  - 数据库系统（DBMS）是指一个能为用户提供信息服务的系统
  - 它实现了有组织地，动态地存储大量相关数据的功能，
  - 提供了数据处理和信息资源共享的便利手段
- 什么是关系型数据库系统？
  - 关系型数据库系统（RDBMS）是指使用了关系模型的数据库系统
  - 关系模型中，数据是分类存放的，数据之间可以有联系  
- 关系型数据库的应用
  - 关系型数据库被应用在非常多的领域：教育系统，商业系统，医疗系统
  - 关系型数据库可以有效组织和管理大量复杂的数据，所以关系型数据库才是最重要的数据库产品
- 主流关系型数据库
  - DB2   Oracle  MySQL  --跨品台    SQL Server  不支持Linux系统，最近才支持
- 什么是NoSQL数据库系统？
  - NoSQL数据库指的是数据分类存放，但是数据之间没有关联关系的数据库系统
- 主流NoSQL数据库
  - Redis     MemCache    MongoDB     Neo4J

### MySQL数据库  

- 安装（尽量下载免费版的安装版本的MSI）

### 什么是SQL语句  

- 数据定义语言：定义逻辑库和数据表
- SQL是用于访问和处理数据的标准计算机语言
- 分类：  
  1.DML（数据操作语言）：添加、修改、删除、查询  
  2.DCL（数据控制语言）：用户、权限、事物  
  3.DDL（数据定义语言）：逻辑库、数据表、视图、索引  
- 注意事项：  
  1.SQL语句不区分大小写，但是字符串区分大小写  
  2.SQL语句必须以分号结尾  
  3.SQL语句中的空白和换行没有限制，但是不能破坏语法  
- SQL注释  
  1. 采用“#”   
     2.使用“/*......*/”  
- 创建逻辑库

```sql
    CREATE  DATABASE 逻辑库名称;
    # 显示逻辑空间
    SHOW DATABASES;
    # 删除逻辑空间
    DROP DATABASE 逻辑表名;
```

- 创建数据表

```sql
    CREATE TABLE  数据表名(
    列名1 数据类型 [约束] [COMMENT 注释], 
    列名1 数据类型 [约束] [COMMENT 注释], 
    ......
    )[COMMENT =  注释];
    # 实例
    CREATE TABLE student(
    id INT UNSIGNED PRIMARY KEY,
    name VARCHAR(20) NOT NULL,
    sex CHAR(1) NOT NULL,
    birthday DATE NOT NULL,
    tel CHAR(11) NOT NULL,
    remark VARCHAR(200)
    );
    
```

- 插入数据  

```sql
    INSERT INTO student VALUES(1,"LIQIAN","MAN","1995-03-23","13112121212",NULL )
```

- 数据表的其他操作  

```sql
   # 展示数据表
    SHOW tables;
    # 展示student表结构
    DESC student;
    # 展示创建数据表student的语句
    SHOW CREATE TABLE sutdent;
    # 删除数据表
    DROP TABLE student
```

- 修改表的结构  

  ```mys
  # 增加字段
  ALTER TABLE 表名称
  ADD 列1 数据类型 [约束] [COMMENT 注释]，
  ADD 列2 数据类型 [约束] [COMMENT 注释]，
  ......;
  # 修改字段数据类型和约束
  ALTER TABLE 表名称
  MODIFY 列1 数据类型 [约束] [COMMENT 注释]，
  MODIFY 列2 数据类型 [约束] [COMMENT 注释]，
  ......;
  # 修改字段名称
  ALTER TABLE 表名称
  CHANGE 列1 数据类型 [约束] [COMMENT 注释]，
  CHANGE 列2 数据类型 [约束] [COMMENT 注释]，
  ......;
  # 删除字段
  ALTER TABLE 表名称
  DROP 列1，
  DROP 列2，
  ......;
  
  ```

### 数据定义语言：字段约束

- 数据库范式
  - 构造数据库必须遵循一定的规则，这种规则就是范式
  - 目前关系数据库有6种范式，一般情况下，只满足第三范式即可  
- 第一范式：原子性
  - 第一范式是数据库的基本要求，不满足这一点的就不是关系数据库
  - 数据表的每一列都是不可分割的基本数据项，同一列中不能有多个值，也不能存在重复属性
- 第二范式：唯一性
  - 数据表种的每条记录必须是唯一的。为了实现区分，通常要为表加上一个列用来存储唯一标识，这个唯一属性列被称作主键列
- 第三范式：关联性
  - 每列都与主键都有直接关系，不存在传递依赖
  - 依照第三范式，数据可以拆分保存到不同的数据表，彼此保持关联
- 字段约束

| 约束名称 | 关键字                 | 描述                         |
| -------- | ---------------------- | ---------------------------- |
| 主键约束 | ＰＲＩＭＡＲＹ　ＫＥＹ | 字段值唯一，且不能为ｎｕｌｌ |
| 非空约束 | ＮＯＴ　ＮＵＬＬ       | 字段值不能为ｎｕｌｌ         |
| 唯一约束 | ＵＮＩＱＵＥ           | 字段值唯一，且可以为ｎｕｌｌ |
| 外键约束 | ＦＯＲＥＩＧＮ　ＫＥＹ | 保持关联数据的逻辑性         |

#### 主键约束

- 主键约束要求字段的值在全表必须唯一，而且不能为ＮＵＬＬ值

- 建议主键一定要使用数字类型，因为数字的检索速度非常快

- 如果主键是数字类型，还可以设置自动增长

  ```mysql
  CREATE TABLE t_teacher(
  	id INT PRIMARY KEY AUTO_INCREMENT,
  	......
  );
  ```

#### 非空约束

- 非空约束要求字段的值不能为NULL值
- NULL值以为没有值，而不是“”空字符串

```mysql
CREATE TABLE t_tacher(
	id INT PROMARY KEY AUTO_INCREMENT,
	name VARCHER(20) NOT NULL,
    married BOOLEAN NOT NULL DEFAULT FALSE
	......
);
```

#### 唯一约束

- 唯一约束要求字段值如果不为NULL，那么在全表必须唯一

```
CREATE TABLE t_teacher(
	......
	tel CHAR(10) NOT NULL UNIQUE
);
```

#### 外键约束

- 外键约束用来保证关联数据的逻辑关系
- 外键约束的定义是写在子表上的

```
# 父表
CREATE TABLE　t_dept(
	deptno INT UNSIGNED PRIMARY KEY,
	dname VARCHER(20) NOT NULL UNIQUE,
	tel CHAR(4) UNIQUE
);

# 子表
CREATE TABLE t_emp(
 empno INT UNSIGED PRIMARY KEY,
 ename VARCHAR(20) NOT NULL,
 sex ENUM("Man","Woman") NOT NULL,
 deptno INT UNSIGNED,
 hiredate DATE NOT NULL,
 FOREIGN KEY (deptno) REFERENCES t_dept(deptno)
);
```

- #### 如果形成外键闭环，我们将无法删除任何一张表的记录



### 数据定义语言（DDL）：索引

#### 数据排序的好处

- 一旦数据排序之后，查找的速度就会翻倍，现实世界跟程序世界都是如此

#### 如何创建索引

```mysql
CREATE TABLE 表名称(
	......,
	INDEX [索引名称]（字段）,
	......
);
# 实例
CREATE TABLE t_message(
	id 	INT UNSIGNED PRIMARY KEY,
	content VARCHAR(200) NOT NULL,
	type ENUM("公告","通报","个人通知") NOT NULL,
	create_time TIMESTAMP NOT NULL,
	INDEX idx_type (type)
);
```

#### 如何添加与删除索引

```mysql
# 添加索引
CREATE INDEX 索引名称 ON 表名（字段）;

ALTER TABLE 表名称 ADD INDEX [索引名]（字段);
# 查看索引
SHOW INDEX FROM 表名;
# 删除索引
DROP INDEX 索引名称 ON 表名;
```

#### 索引的使用原则

- 数据量很大，而且经常被查询的数据表可以设置索引
- 索引只添加在经常被用作检索条件的字段上面
- 不要在大字段上创建索引（一般超过50个字符就不适合创建索引）





## 数据库的基本查询

### 数据的简单查询

- 无条件查询记录，字段的计算和字段的别名



### 数据的高级查询

- 数据排序，分页，去除重复项



### 数据的有条件查询

- 条件表达式：数学运算符，比较运算符，逻辑运算符，按位运算符

### 

### 
