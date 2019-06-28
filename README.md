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





## 数据库的基本查询(使用demo.sql)

### 数据的简单查询

- 无条件查询记录，字段的计算和字段的别名



### 数据的高级查询

- 数据排序，分页，去除重复项



### 数据的有条件查询

- 条件表达式：数学运算符，比较运算符，逻辑运算符，按位运算符



#### 记录查询

- 最基本的查询语句是有SELECT和FROM关键字组成的

```mysql
SELECT * FROOM t_emp;

SELECT empno,ename,sal FROM t_emp;
```

- SELECT语句屏蔽了物理层的操作，用户不必关心数据的真实存储，交由数据库高效的查找数据
- 通常情况下，SELECT子句中使用了表达式，那么这列的 别名就默认为表达式，因此需要一种对列名重命名的机制

```mysql
SELECT
	empno,
	sal*12 AS "income"
FROM t_emp;
```

- 查询语句的子句执行顺序

```mysql
# 1.词法分析与优化 读取SQL语句
# 2.FROM 选择数据来源
# 3.SELECT 选择输出内容
SELECT
	empno,
	sal*12 AS "income"
FROM t_emp;
```

#### 数据操作语言：数据分页

- 比如我们查看朋友圈，只会加载少量部分信息，不用一次性加载全部朋友圈，那样只会浪费CPU时间、内存和网络带宽
- 如果结果集的记录很多，则可以使用LIMIT关键字限定结果集数量

```mysql
SELECT ...... FROM...... LIMIT 起始位置，偏移量;
# 举例
SELECT empno,ename FROM t_emp LIMIT 0,20;
```

- 数据分页的简写用法

  - 如果LIMIT子句只有一个参数，它表示的是偏移量，起始值默认为0

  ```mysql
  SELECT empno,ename FROM t_tmp LIMIT 10;
  SELECT empno,ename FROM t-tmp LIMIT 0,10;
  
  # 执行顺序
  FROM 》》 SELECT 》》 LIMIT
  
  ```

#### 数据操作语言：结果集排序

- 如果没有设置，查询语句不会对结果集进行排序。也就是说，如果想让结果集按照某种顺序排列，就必须使用ORDER BY子句

```mysql
# 语句格式
SELECT ...... FROM ...... ORDER BY 列名 [ASC|DESC];
# 举例(默认为[ASC]升序,降序[DESC])
SELECT ename,sal FROM t_tmp ORDER BY sal;
```

- ASC代表升序（默认），DESC代表降序
- 如果排序列是数字类型，数据库就按照数字大小排序，如果是日期类型就按照日期大小排序，如果是字符串就按照字符集序号排序

#### 多个排序字段

- 默认情况下，如果两条数据排序字段内容相同，那么排序会是什么样子

- 我们可以使用ORDER BY 规定首要排序条件和子要排序条件，数据库会按照首要排序条件排序，如果遇到首要排序内容相同的记录，那么就会启用次要排序条件接着排序

```
# 语句格式
SELECT ...... FROM ...... ORDER BY 列名 [ASC|DESC],列名 [ASC|DESC];
# 举例(默认为[ASC]升序,降序[DESC])
SELECT ename,sal FROM t_tmp ORDER BY sal DESC,hiredate ASC;
```

- ORDER BY 与LIMIT联合

```mysql
# 查询出empno,ename,sal并按照sal排列出前5
SELECT
	empno,ename,asl
FROM t_emp ORDER BY sal DESC LIMIT 0,5;
```

#### 排序+分页

- ORDER BY子句书写的时候放在LIMIT子句的前面

```mysql
# 执行顺序
FROM >> SELECT >> ORDER BY >> LIMIT
```

#### 数据操作语言：去除重复记录

##### 结果集中的重复记录

- 假如我们要查询员工表有多少种职业，写出来的SQL语句如下：`SELECT job FROM t_tmp;`

- 如果我们需要去除冲覅的数据，可以使用DISTINCT关键字实现（只去除结果集的，不会该表数据库）：`SELECT DISTINCT 字段 FROM .....;`
- 去掉job字段集中的重复记录：`SELECT DISTINCT job FROM t_tmp；`

##### 注意事项

- 使用DISTINCT的SELECT子句中只能查询一列数据，如果查询多列，去除重复记录就会失效
- DISTINCT关键字只能在SELECT子句中使用一次

#### 数据操作语言：条件查询（一）

- 很多时候，用户感兴趣的并不是逻辑表里的全部记录，而只是它们当中能够满足某一种或几种条件的记录。这类条件要用WHERE子句来实现数据的筛选`SELECT ... FROM ... WHERE 条件 [AND|OR] 条件 ...;` 

- 四类运算符

| 序号 |   运算符   |
| :--: | :--------: |
|  1   | 数学运算符 |
|  2   | 比较运算符 |
|  3   | 逻辑运算符 |
|  4   | 换位运算符 |

- 算数运算符

| 序号 | 表达式 | 意义 | 例子 |
| :--: | :----: | :--: | :--: |
|  1   |   +    | 加法 |      |
|  2   |   -    | 减法 |      |
|  3   |   *    | 乘法 |      |
|  4   |   /    | 除法 |      |
|  5   |   %    | 求模 |      |

- 比较运算符

| 序号 |   表达式    |       意义       |
| :--: | :---------: | :--------------: |
|  1   |      >      |       大于       |
|  2   |     >=      |     大于等于     |
|  3,  |     <=      |       小于       |
|  4   |     <=      |     小于等于     |
|  5   |      =      |       等于       |
|  6   |     !=      |      不等于      |
|  7   |     IN      |       包含       |
|  8   |  IS　NULL   |       为空       |
|  9   | IS NOT NULL |      不为空      |
|  10  | BETWEEN AND | 范围（包含左右） |
|  11  |    LIKE     |     模糊查询     |
|  12  |   REGEXP    |    正则表达式    |

- 逻辑运算符

| 序号 | 表达式 |   意义   |
| :--: | :----: | :------: |
|      |  AND   |  与关系  |
|  2   |   OR   |  或关系  |
|  3   |  NOT   |  非关系  |
|  4   |  XOR   | 异或关系 |

##### 二进制按位运算

- 二进制位运算的实质是指将参与运算的两个操作数，按对应的二进制数逐位进行逻辑运算

- 按位运算符

| 序号 | 表达式 |   意义   |
| :--: | :----: | :------: |
|  1   |   &    | 位与关系 |
|  2   |   \|   | 位或关系 |
|  3   |   ~    |  位取反  |
|  4   |   ^    |  位异或  |
|  5   |   <<   |   左移   |
|  6   |   >>   |   右移   |



### WHERE子句的注意事项

- WHERE子句中，条件执行的顺序是从左到右的。所以我们应该把索引条件，或者筛选掉记录最多的条件写在最左侧。

```mysql
SELECT empno,ename FROM t_tmp
WHERE ename = "FORD" AND sal>=2000;

SELECT empno,ename FROM t_tmp
WHERE deptno = 10 and sal >= 2000;
```

#### 各种子句的执行顺序

- 条件查询中，WHERE子句应该是第几个执行的额？

```
FROM -> WHER -> SELECT -> ORDER BY ->LIMIT 
```



## 数据库的高级查询

- 数据统计分析
  - 聚合函数、分组查询、HAVING子句

- 多表连接查询
  - 内连接，外连接、以及多表查询的多种语法
- 子查询
  - 单行子查询、多行子查询、WHERE子查询、FROM子查询、SELECT子查询

#### 数据操作语言：聚合函数(永远不能出现在WHERE子句中)

- 聚合函数在数据的查询分析中，应用十分广泛。聚合函数可以对数据求和、求最大值和最小值、求平均值等等。

- SUM函数用于求和，只能用于数字类型，字符类型的统计结果为0，日期类型统计结果是毫秒数相加

```mysql
SELECT SUM(ename) FROM t_tmp;

SELECT SUM(sal) FROM t_tmp
WHERE deptno IN (10,20);
```

- MAX函数用于获得非空值的最大值

```
# 基本语法
SELECT MAX(comm) FROM t_emp;
# 问题1：查询10和20部门中，月收入最高的员工？
SELECT MAX(sal + IFNULL(comm,0)) FROM t_tmp WHERE deptno IN(10,20);
# 问题2：查询员工名字最长的是几个字符？
SELECT MAX(LENGTH(ename)) FROM t_tmp;
```

- MIN函数用于获得非空值的最大值

```
# 基本语法
SELECT MIN(comm) FROM t_emp;
# 问题1：查询10和20部门中，月收入最低的员工？
SELECT MIN(sal + IFNULL(comm,0)) FROM t_tmp WHERE deptno IN(10,20);
# 问题2：查询员工名字最短的是几个字符？
SELECT MIN(LENGTH(ename)) FROM t_tmp;
```

- AVG函数用于获取非空值的平均值，非数字数据统计结果为0
- COUNT函数：COUNT(*)用于获得包含空值的记录数，COUNT(列名)用于获得包含非空值的记录数

```mysql
# COUNT(*)
SELECT COUNT(*) FORM t_emp;

# COUNT(字段名)
SELECT COUNT(comm) FROM t-emp;

# 查询10和20部门中，底薪超过2000元并且工龄超过15年的员工人数
SELECT COUNT(*) FROM t_tmp WHERE deptno in(10,20) and (sal+ifnull(comm,0))>=2000 and (now()-hiredate)>15;

# 查询1985年以后入职的员工，底薪超过公司平均底薪的员工数量？
SELECT 
	COUNT(*) 
FROM 
	t_emp 
WHERE
	hiredate>="1995-01-01"
AND
	sal >= SELECT AVG(sal+ifnull(comm,0)) FROM t_emp;
```



#### 数据操作语言：分组查询

- 为什么要分组？

  - 默认情况下汇总函数是对全表范围内的数据做统计
  - GROUP BY子句的作用是通过一定的规则将一个数据集划分成若干个小的区域，然后针对每个小区域分别进行数据汇总处理

  ```mysql
  # ROUND()将小数四舍五入成整数
  SELECT deptno,ROUND(AVG(sal)) FROM t_emp GROUP BY deptno;
  ```

- 逐级分组

  - 数据库支持多列分组条件，执行的时候逐级分组

  ```mysql
  # 查询每个部门里，每种职位的人员数量和平均底薪
  SELECT deptno,job,COUNT(*),AVG(sal) FROM t_emp GROUP BY deptno,job,ORDER BY deptno;
  ```

  
