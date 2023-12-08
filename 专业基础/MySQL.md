
配合教学视频食用口味更佳：  
[《黑马程序员 Mysql数据库入门到精通》](https://www.bilibili.com/video/BV1Kr4y1i7ru)  

# 基础篇

## 概念

|      名称     | 解释                                | 英文名称                         |
|     数据库    | 存储数据的仓库，数据是有组织地进行存储 | DataBase(DB)                     |
| 数据库管理系统 | 操纵和管理数据库的大型软件            | DataBase Management System(DBMS) |
|      SQL      | 操作关系型数据库的编程语言            | Structured Query Language(SQL)   |

关系数据库系统是支持关系模型的数据库系统，SQL是关系数据库的标准语言，Mysql是一个主流的关系型数据库操作系统之一。  
关系模型可以认为是二维表。  

### 基础概念

| 概念       | 解释 |
| ---------- | --- |
| 关系        | 可以理解为一张二维表, 关系名就是表名 |  
| 元组        | 二维表中的一行, 数据库中称为记录 | 
| 属性        | 二维表中的一列, 数据库中称为字段 |
| 域          | 属性的取值范围, 即数据库中字段的取值限制 |
| 候选码      | 一组能唯一标识一个元组的属性组, 而其子集不能 |
| 主码(键)    | 若一个关系又多个候选码, 则选定其中一个为主码 |
| 主属性      | 候选码所包含的属性 |
| 非主(码)属性 | 不包含在任何候选码中的属性 |
| 全码        | 关系模式的所有属性是这个关系模式的候选码 |
| 关系模式     | 指对关系的描述 |  



### 关系模式

R(U, D, DOM, F)

- R: 关系名
- U: 组成该关系的属性名集合
- D: 属性组U中的属性的域
- DOM: 属性到域的映射集合
- F: 属性间数据的依赖关系集合

例:
```
student(U, D, DOM, F)  
U = {studentID, name, gender, department}  
D: D1={任意10个数字字符组成的字符串},D2={任意汉字},D3={男,女},D4={学校开设的院系}  
DOM: DOM(studentID)=D1, DOM(name)=D2, ...  
F: studentID -> name, studentID -> gender, studentID -> department
```

### 关系的完整性

1. 实体完整性: 主属性不能为空.  
2. 参照完整性: 外键不为空时, 其值必须在其关联的表中存在.  
3. 用户定义的完整性: 指用户定义的对关系中某属性自定义的约束规则.  

### 关系代数

关系代数是一种抽象的查询语言, 它用对关系的运算来表达查询.  
可分为传统的集合运算和专门的关系运算.  

| 运算 | 表示 |
| --- | --- |
| 并(union) | RUS = {t \| t∈R ∨ t∈S} |
| 差(except) | R-S = {t \| t∈R ∧ t∉S} |
| 交(intersection) | R∩S = {t \| t∈R ∧ t∈S} |
| 笛卡儿积(cartesian product) | ... |
| 选择(select) | σF(R) = {t \| t∈R ∧ F(t) = 'true'} |
| 投影(projection) | ΠA(R) = {t[A] \| t∈R}, A为R中的列属性 |
| 连接(join) | 从笛卡尔积中选其一定条件的元组 |
| 除运算(division) | 详细解释见下文 |

- 等值连接: 选择两属性值相等的进行连接, 自然连接要求属性名相同. 
	悬浮元组: 如果选择的属性值只在一张表中存在, 进行等值连接时, 这些元组就会被舍弃, 称其为悬浮元组.  
	外连接: 保存全部悬浮元组, 空属性赋值为null.  
	左外连接: 只保留左表中的悬浮元组.  
	右外连接: 只保留右表中的悬浮元组.  
	内连接: 不保留悬浮元组, 就是普通的等值连接.  

- 除运算: 
	设关系R除以关系S的结果为关系T, 则关系T包含所有在R但不在S的中的属性及其值, 且T的元组与S的元的所有组合(笛卡儿积)都在R中.  

### 模式

- 模式(schema): 对数据库中全体数据的逻辑结构和特征的描述, 可以理解为一个数据库.
- 外模式(external schema): 客户所能看到的结果(视图).
- 内模式(internal schema): 数据的物理存储结构和存储方式. 

-----

## 通用语法及分类

- DDL: 数据定义语言，用来定义数据库对象（数据库、表、字段）
- DML: 数据操作语言，用来对数据库表中的数据进行增删改
- DQL: 数据查询语言，用来查询数据库中表的记录
- DCL: 数据控制语言，用来创建数据库用户、控制数据库的控制权限

### DDL（数据定义语言）

#### 数据库操作

查询所有数据库：  
`SHOW DATABASES;`  
查询当前数据库：  
`SELECT DATABASE();`  
创建数据库：  
`CREATE DATABASE [ IF NOT EXISTS ] 数据库名 [ DEFAULT CHARSET 字符集] [COLLATE 排序规则 ];`  
删除数据库：  
`DROP DATABASE [ IF EXISTS ] 数据库名;`  
使用数据库：  
`USE 数据库名;`  

##### 注意事项

- UTF8字符集长度为3字节，有些符号占4字节，所以推荐用utf8mb4字符集

#### 表操作

查询当前数据库所有表：  
`SHOW TABLES;`  
查询表结构：  
`DESC 表名;`  
查询指定表的建表语句：  
`SHOW CREATE TABLE 表名;`  

创建表：
```sql
CREATE TABLE 表名(
	字段1 字段1类型 [COMMENT 字段1注释],
	字段2 字段2类型 [COMMENT 字段2注释],
	字段3 字段3类型 [COMMENT 字段3注释],
	...
	字段n 字段n类型 [COMMENT 字段n注释]
)[ COMMENT 表注释 ];
```
**最后一个字段后面没有逗号**

添加字段：  
`ALTER TABLE 表名 ADD 字段名 类型(长度) [COMMENT 注释] [约束];`  
例：`ALTER TABLE emp ADD nickname varchar(20) COMMENT '昵称';`

修改数据类型：  
`ALTER TABLE 表名 MODIFY 字段名 新数据类型(长度);`

修改字段名和字段类型：  
`ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型(长度) [COMMENT 注释] [约束];`  
例：将emp表的nickname字段修改为username，类型为varchar(30)  
`ALTER TABLE emp CHANGE nickname username varchar(30) COMMENT '昵称';`

删除字段：  
`ALTER TABLE 表名 DROP 字段名;`

修改表名：  
`ALTER TABLE 表名 RENAME TO 新表名`

删除表：  
`DROP TABLE [IF EXISTS] 表名;`  
删除表，并重新创建该表：  
`TRUNCATE TABLE 表名;`

### DML（数据操作语言）

#### 添加数据

指定字段：  
`INSERT INTO 表名 (字段名1, 字段名2, ...) VALUES (值1, 值2, ...);`  
全部字段：  
`INSERT INTO 表名 VALUES (值1, 值2, ...);`

批量添加数据：
```sql
INSERT INTO 表名 (字段名1, 字段名2, ...)  
VALUES (值1, 值2, ...), (值1, 值2, ...), (值1, 值2, ...);

INSERT INTO 表名 VALUES (值1, 值2, ...), (值1, 值2, ...), (值1, 值2, ...);
```

##### 注意事项

- 字符串和日期类型数据应该包含在引号中
- 插入的数据大小应该在字段的规定范围内

#### 更新和删除数据

修改数据：  
`UPDATE 表名 SET 字段名1 = 值1, 字段名2 = 值2, ... [ WHERE 条件 ];`  
例：  
`UPDATE emp SET name = 'Jack' WHERE id = 1;`

删除数据：  
`DELETE FROM 表名 [ WHERE 条件 ];`

### DQL（数据查询语言）

语法：
```sql
SELECT
	字段列表
FROM
	表名字段
WHERE
	条件列表
GROUP BY
	分组字段列表
HAVING
	分组后的条件列表
ORDER BY
	排序字段列表
LIMIT
	分页参数
```

#### 基础查询

查询多个字段：  
`SELECT 字段1, 字段2, 字段3, ... FROM 表名;`  
`SELECT * FROM 表名;`

设置别名：  
`SELECT 字段1 [ AS 别名1 ], 字段2 [ AS 别名2 ], 字段3 [ AS 别名3 ], ... FROM 表名;`  
`SELECT 字段1 [ 别名1 ], 字段2 [ 别名2 ], 字段3 [ 别名3 ], ... FROM 表名;`

去除重复记录：  
`SELECT DISTINCT 字段列表 FROM 表名;`

转义：  
`SELECT * FROM 表名 WHERE name LIKE '/_张三' ESCAPE '/'`  
/ 之后的\_不作为通配符

#### 条件查询

语法：  
`SELECT 字段列表 FROM 表名 WHERE 条件列表;`

条件：

| 比较运算符          | 功能                                        |
| ------------------- | ------------------------------------------- |
| >                   | 大于                                        |
| >=                  | 大于等于                                    |
| <                   | 小于                                        |
| <=                  | 小于等于                                    |
| =                   | 等于                                        |
| <> 或 !=            | 不等于                                      |
| BETWEEN ... AND ... | 在某个范围内（含最小、最大值）              |
| IN(...)             | 在in之后的列表中的值，多选一                |
| LIKE 占位符         | 模糊匹配（\_匹配单个字符，%匹配任意个字符） |
| IS NULL             | 是NULL                                      |

| 逻辑运算符         | 功能                         |
| ------------------ | ---------------------------- |
| AND 或 &&          | 并且（多个条件同时成立）     |
| OR 或 &#124;&#124; | 或者（多个条件任意一个成立） |
| NOT 或 !           | 非，不是                     |

例子：
```sql
-- 年龄等于30
select * from employee where age = 30;
-- 年龄小于30
select * from employee where age < 30;
-- 小于等于
select * from employee where age <= 30;
-- 没有身份证
select * from employee where idcard is null or idcard = '';
-- 有身份证
select * from employee where idcard;
select * from employee where idcard is not null;
-- 不等于
select * from employee where age != 30;
-- 年龄在20到30之间
select * from employee where age between 20 and 30;
select * from employee where age >= 20 and age <= 30;
-- 下面语句不报错，但查不到任何信息
select * from employee where age between 30 and 20;
-- 性别为女且年龄小于30
select * from employee where age < 30 and gender = '女';
-- 年龄等于25或30或35
select * from employee where age = 25 or age = 30 or age = 35;
select * from employee where age in (25, 30, 35);
-- 姓名为两个字
select * from employee where name like '__';
-- 身份证最后为X
select * from employee where idcard like '%X';
```

#### 聚合查询（聚合函数）

常见聚合函数：

| 函数  | 功能     |
| ----- | -------- |
| count | 统计数量 |
| max   | 最大值   |
| min   | 最小值   |
| avg   | 平均值   |
| sum   | 求和     |

语法：  
`SELECT 聚合函数(字段列表) FROM 表名;`  
例：  
`SELECT count(id) from employee where workaddress = "广东省";`

#### 分组查询

语法：  
`SELECT 字段列表 FROM 表名 [ WHERE 条件 ] GROUP BY 分组字段名 [ HAVING 分组后的过滤条件 ];`

where 和 having 的区别：

- 执行时机不同：where是分组之前进行过滤，不满足where条件不参与分组；having是分组后对结果进行过滤。
- 判断条件不同：where不能对聚合函数进行判断，而having可以。

例子：

```sql
-- 根据性别分组，统计男性和女性数量（只显示分组数量，不显示哪个是男哪个是女）
select count(*) from employee group by gender;
-- 根据性别分组，统计男性和女性数量
select gender, count(*) from employee group by gender;
-- 根据性别分组，统计男性和女性的平均年龄
select gender, avg(age) from employee group by gender;
-- 年龄小于45，并根据工作地址分组
select workaddress, count(*) from employee where age < 45 group by workaddress;
-- 年龄小于45，并根据工作地址分组，获取员工数量大于等于3的工作地址
select workaddress, count(*) address_count from employee where age < 45 group by workaddress having address_count >= 3;
```

##### 注意事项

- 执行顺序：where > 聚合函数 > having
- 分组之后，查询的字段一般为聚合函数和分组字段，查询其他字段无任何意义

#### 排序查询

语法：  
`SELECT 字段列表 FROM 表名 ORDER BY 字段1 排序方式1, 字段2 排序方式2;`

排序方式：

- ASC: 升序（默认）
- DESC: 降序

例子：

```sql
-- 根据年龄升序排序
SELECT * FROM employee ORDER BY age ASC;
SELECT * FROM employee ORDER BY age;
-- 两字段排序，根据年龄升序排序，入职时间降序排序
SELECT * FROM employee ORDER BY age ASC, entrydate DESC;
```

##### 注意事项

如果是多字段排序，当第一个字段值相同时，才会根据第二个字段进行排序

#### 分页查询

语法：  
`SELECT 字段列表 FROM 表名 LIMIT 起始索引, 查询记录数;`

例子：

```sql
-- 查询第一页数据，展示10条
SELECT * FROM employee LIMIT 0, 10;
-- 查询第二页
SELECT * FROM employee LIMIT 10, 10;
```

##### 注意事项

- 起始索引从0开始，起始索引 = （查询页码 - 1） * 每页显示记录数
- 分页查询是数据库的方言，不同数据库有不同实现，MySQL是LIMIT
- 如果查询的是第一页数据，起始索引可以省略，直接简写 LIMIT 10

#### DQL执行顺序

FROM -> WHERE -> GROUP BY -> SELECT -> ORDER BY -> LIMIT

### DCL（数据控制语言）

#### 管理用户

查询用户：

```sql
USE mysql;
SELECT * FROM user;
```

创建用户:  
`CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';`

修改用户密码：  
`ALTER USER '用户名'@'主机名' IDENTIFIED WITH mysql_native_password BY '新密码';`

删除用户：  
`DROP USER '用户名'@'主机名';`

例子：

```sql
-- 创建用户test，只能在当前主机localhost访问
create user 'test'@'localhost' identified by '123456';
-- 创建用户test，能在任意主机访问
create user 'test'@'%' identified by '123456';
create user 'test' identified by '123456';
-- 修改密码
alter user 'test'@'localhost' identified with mysql_native_password by '1234';
-- 删除用户
drop user 'test'@'localhost';
```

##### 注意事项

- 主机名可以使用 % 通配

#### 权限控制

常用权限：

| 权限                | 说明               |
| ------------------- | ------------------ |
| ALL, ALL PRIVILEGES | 所有权限           |
| SELECT              | 查询数据           |
| INSERT              | 插入数据           |
| UPDATE              | 修改数据           |
| DELETE              | 删除数据           |
| ALTER               | 修改表             |
| DROP                | 删除数据库/表/视图 |
| CREATE              | 创建数据库/表      |

更多权限请看[权限一览表](#权限一览表 "权限一览表")

查询权限：  
`SHOW GRANTS FOR '用户名'@'主机名';`

授予权限：  
`GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名' [with grant option];`  
带有 'with grant option'时用户可以将其权限授予其他用户。

撤销权限：  
`REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名';`

##### 注意事项

- 多个权限用逗号分隔
- 授权时，数据库名和表名可以用 * 进行通配，代表所有
- 不同表格需要分开写

#### 创建角色(MySQL8.0)

数据库角色是被命名的一组与数据库操作相关的权限，角色是权限的集合。

创建角色:  
`create role '角色名';`

给角色授权:  
`grant 权限列表 on 对象类型(表格) 对象名 to 角色名;`

将角色授予其他角色或用户:  
`grant 角色列表 to 角色或用户列表 [with admin option];`

角色权限回收:  
`revoke 权限列表 on 对象类型 对象名 from 角色列表;`

---

## 函数

- 字符串函数
- 数值函数
- 日期函数
- 流程函数

### 字符串函数

常用函数：

| 函数  | 功能  |
| ------------ | ------------ |
| CONCAT(s1, s2, ..., sn)  | 字符串拼接，将s1, s2, ..., sn拼接成一个字符串  |
| LOWER(str)  | 将字符串全部转为小写  |
| UPPER(str)  | 将字符串全部转为大写  |
| LPAD(str, n, pad)  | 左填充，用字符串pad对str的左边进行填充，达到n个字符串长度  |
| RPAD(str, n, pad)  | 右填充，用字符串pad对str的右边进行填充，达到n个字符串长度  |
| TRIM(str)  | 去掉字符串头部和尾部的空格  |
| SUBSTRING(str, start, len)  | 返回从字符串str从start位置起的len个长度的字符串  |
| REPLACE(column, source, replace)  | 替换字符串  |

使用示例：

```sql
-- 拼接
SELECT CONCAT('Hello', 'World');
-- 小写
SELECT LOWER('Hello');
-- 大写
SELECT UPPER('Hello');
-- 左填充
SELECT LPAD('01', 5, '-');
-- 右填充
SELECT RPAD('01', 5, '-');
-- 去除空格
SELECT TRIM(' Hello World ');
-- 切片（起始索引为1）
SELECT SUBSTRING('Hello World', 1, 5);
```

### 数值函数

常见函数：

| 函数  | 功能  |
| ------------ | ------------ |
| CEIL(x)  | 向上取整  |
| FLOOR(x)  | 向下取整  |
| MOD(x, y)  | 返回x/y的模  |
| RAND() | 返回0~1内的随机数 |
| ROUND(x, y) | 求参数x的四舍五入值，保留y位小数 |

### 日期函数

常用函数：

| 函数  | 功能  |
| ------------ | ------------ |
| CURDATE()  | 返回当前日期  |
| CURTIME()  | 返回当前时间  |
| NOW()  | 返回当前日期和时间  |
| YEAR(date)  | 获取指定date的年份  |
| MONTH(date)  | 获取指定date的月份  |
| DAY(date)  | 获取指定date的日期  |
| DATE_ADD(date, INTERVAL expr type)  | 返回一个日期/时间值加上一个时间间隔expr后的时间值  |
| DATEDIFF(date1, date2)  | 返回起始时间date1和结束时间date2之间的天数  |

例子：

```sql
-- DATE_ADD
SELECT DATE_ADD(NOW(), INTERVAL 70 YEAR);
```

### 流程函数

常用函数：

| 函数  | 功能  |
| ------------ | ------------ |
| IF(value, t, f)  | 如果value为true，则返回t，否则返回f  |
| IFNULL(value1, value2)  | 如果value1不为空，返回value1，否则返回value2  |
| CASE WHEN [ val1 ] THEN [ res1 ] ... ELSE [ default ] END  | 如果val1为true，返回res1，... 否则返回default默认值  |
| CASE [ expr ] WHEN [ val1 ] THEN [ res1 ] ... ELSE [ default ] END  | 如果expr的值等于val1，返回res1，... 否则返回default默认值  |

例子：

```sql
select
	name,
	(case when age > 30 then '中年' else '青年' end)
from employee;
select
	name,
	(case workaddress when '北京市' then '一线城市' when '上海市' then '一线城市' else '二线城市' end) as '工作地址'
from employee;
```

---

## 约束

分类：

| 约束  | 描述  | 关键字  |
| ------------ | ------------ | ------------ |
| 非空约束  | 限制该字段的数据不能为null  | NOT NULL  |
| 唯一约束  | 保证该字段的所有数据都是唯一、不重复的  | UNIQUE  |
| 主键约束  | 主键是一行数据的唯一标识，要求非空且唯一  | PRIMARY KEY  |
| 默认约束  | 保存数据时，如果未指定该字段的值，则采用默认值  | DEFAULT  |
| 检查约束（8.0.16版本后）  | 保证字段值满足某一个条件  | CHECK  |
| 外键约束  | 用来让两张图的数据之间建立连接，保证数据的一致性和完整性  | FOREIGN KEY  |

约束是作用于表中字段上的，可以再创建表/修改表的时候添加约束。

### 常用约束

| 约束条件  | 关键字  |
| ------------ | ------------ |
| 主键  | PRIMARY KEY  |
| 自动增长  | AUTO_INCREMENT  |
| 不为空  | NOT NULL  |
| 唯一  | UNIQUE  |
| 逻辑条件  | CHECK  |
| 默认值  | DEFAULT  |

元组约束:

在create table时用 check 短语定义元组约束,可以定义不同属性之间的约束条件。

例子：

```sql
create table user(
	id int primary key auto_increment,
	name varchar(10) not null unique,
	age int check(age > 0 and age < 120),
	status char(1) default '1',
	gender char(1) check(gender in ('男','女') )
	check (...) //元组约束
);
```

约束命名句子:

在属性后面添加`constraint '约束名' <约束条件>;`  
从而灵活地增加、删除约束条件。  
`alter table '表名' 'add/drop' constraint '约束名' <约束条件>;`

### 外键约束

添加外键：

```sql
CREATE TABLE 表名(
	字段名 字段类型,
	...
	[CONSTRAINT] [外键名称] FOREIGN KEY(外键字段名) REFERENCES 主表(主表列名)
);
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名) REFERENCES 主表(主表列名);

-- 例子
alter table emp add constraint fk_emp_dept_id foreign key(dept_id) references dept(id);
```

删除外键：  
`ALTER TABLE 表名 DROP FOREIGN KEY 外键名;`

#### 删除/更新行为

| 行为  | 说明  |
| ------------ | ------------ |
| NO ACTION  | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新（与RESTRICT一致）  |
| RESTRICT  | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新（与NO ACTION一致）  |
| CASCADE  | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则也删除/更新外键在子表中的记录  |
| SET NULL  | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则设置子表中该外键值为null（要求该外键允许为null）  |
| SET DEFAULT  | 父表有变更时，子表将外键设为一个默认值（Innodb不支持）  |

更改删除/更新行为(先删除再重新添加):  
`ALTEE TABLE 表名 DROP CONSTRAINT 外键名;`  
`ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段) REFERENCES 主表名(主表字段名) ON UPDATE 行为 ON DELETE 行为;`

---

## 多表查询

### 多表关系

- 一对多（多对一）
- 多对多
- 一对一

#### 一对多

案例：部门与员工  
关系：一个部门对应多个员工，一个员工对应一个部门  
实现：在多的一方建立外键，指向一的一方的主键  

#### 多对多

案例：学生与课程  
关系：一个学生可以选多门课程，一门课程也可以供多个学生选修  
实现：建立第三张中间表，中间表至少包含两个外键，分别关联两方主键  

#### 一对一

案例：用户与用户详情  
关系：一对一关系，多用于单表拆分，将一张表的基础字段放在一张表中，其他详情字段放在另一张表中，以提升操作效率  
实现：在任意一方加入外键，关联另外一方的主键，并且设置外键为唯一的（UNIQUE）  

### 查询

合并查询（笛卡尔积，会展示所有组合结果）：  
`select * from employee, dept;`

> 笛卡尔积：两个集合A集合和B集合的所有组合情况（在多表查询时，需要消除无效的笛卡尔积）

消除无效笛卡尔积：  
`select * from employee, dept where employee.dept = dept.id;`

### 内连接查询

内连接查询的是两张表交集的部分

隐式内连接：  
`SELECT 字段列表 FROM 表1, 表2 WHERE 条件 ...;`

显式内连接：  
`SELECT 字段列表 FROM 表1 [ INNER ] JOIN 表2 ON 连接条件 ...;`

显式性能比隐式高

例子：

```sql
-- 查询员工姓名，及关联的部门的名称
-- 隐式
select e.name, d.name from employee as e, dept as d where e.dept = d.id;
-- 显式
select e.name, d.name from employee as e inner join dept as d on e.dept = d.id;
```

- 为表格起别名: 表名 [as] 别名, as 可省略. 

### 外连接查询

左外连接：  
查询左表所有数据，以及两张表交集部分数据  
`SELECT 字段列表 FROM 表1 LEFT [ OUTER ] JOIN 表2 ON 条件 ...;`  
相当于查询表1的所有数据，包含表1和表2交集部分数据

右外连接：  
查询右表所有数据，以及两张表交集部分数据  
`SELECT 字段列表 FROM 表1 RIGHT [ OUTER ] JOIN 表2 ON 条件 ...;`

例子：

```sql
-- 左
select e.*, d.name from employee as e left outer join dept as d on e.dept = d.id;
select d.name, e.* from dept d left outer join emp e on e.dept = d.id;  -- 这条语句与下面的语句效果一样
-- 右
select d.name, e.* from employee as e right outer join dept as d on e.dept = d.id;
```

左连接可以查询到没有dept的employee，右连接可以查询到没有employee的dept

### 自连接查询

当前表与自身的连接查询，自连接必须使用表别名

语法：  
`SELECT 字段列表 FROM 表A 别名A JOIN 表A 别名B ON 条件 ...;`

自连接查询，可以是内连接查询，也可以是外连接查询

例子：

```sql
-- 查询员工及其所属领导的名字
select a.name, b.name from employee a, employee b where a.manager = b.id;
-- 没有领导的也查询出来
select a.name, b.name from employee a left join employee b on a.manager = b.id;
```

### 联合查询 union, union all

把多次查询的结果合并，形成一个新的查询集

语法：

```sql
SELECT 字段列表 FROM 表A ...
UNION [ALL]
SELECT 字段列表 FROM 表B ...
```

#### 注意事项

- UNION ALL 会有重复结果，UNION 不会
- 联合查询比使用or效率高，不会使索引失效
- 两个字段列表需一致

### 子查询

SQL语句中嵌套SELECT语句，称谓嵌套查询，又称子查询。  
`SELECT * FROM t1 WHERE column1 = ( SELECT column1 FROM t2);`  
**子查询外部的语句可以是 INSERT / UPDATE / DELETE / SELECT 的任何一个**

根据子查询结果可以分为：

- 标量子查询（子查询结果为单个值）
- 列子查询（子查询结果为一列）
- 行子查询（子查询结果为一行）
- 表子查询（子查询结果为多行多列）

根据子查询位置可分为：

- WHERE 之后
- FROM 之后
- SELECT 之后

#### 标量子查询

子查询返回的结果是单个值（数字、字符串、日期等）。  
常用操作符：- < > > >= < <=

例子：

```sql
-- 查询销售部所有员工
select id from dept where name = '销售部';
-- 根据销售部部门ID，查询员工信息
select * from employee where dept = 4;
-- 合并（子查询）
select * from employee where dept = (select id from dept where name = '销售部');

-- 查询xxx入职之后的员工信息
select * from employee where entrydate > (select entrydate from employee where name = 'xxx');
```

#### 列子查询

返回的结果是一列（可以是多行）。

常用操作符：

| 操作符  | 描述  |
| ------------ | ------------ |
| IN  | 在指定的集合范围内，多选一  |
| NOT IN  | 不在指定的集合范围内  |
| ANY  | 子查询返回列表中，有任意一个满足即可  |
| SOME  | 与ANY等同，使用SOME的地方都可以使用ANY  |
| ALL  | 子查询返回列表的所有值都必须满足  |

例子：

```sql
-- 查询销售部和市场部的所有员工信息
select * from employee where dept in (select id from dept where name = '销售部' or name = '市场部');
-- 查询比财务部所有人工资都高的员工信息
select * from employee where salary > all(select salary from employee where dept = (select id from dept where name = '财务部'));
-- 查询比研发部任意一人工资高的员工信息
select * from employee where salary > any (select salary from employee where dept = (select id from dept where name = '研发部'));
```

#### 行子查询

返回的结果是一行（可以是多列）。  
常用操作符：=, <, >, IN, NOT IN

例子：

```sql
-- 查询与xxx的薪资及直属领导相同的员工信息
select salary, manager from employee where name = 'xxx';
select * from employee where (salary, manager) = (select salary, manager from employee where name = 'xxx');
```

#### 表子查询

返回的结果是多行多列  
常用操作符：IN

例子：

```sql
-- 查询与xxx1，xxx2的职位和薪资相同的员工
select * from employee where (job, salary) in (select job, salary from employee where name = 'xxx1' or name = 'xxx2');
-- 查询入职日期是2006-01-01之后的员工，及其部门信息
select e.*, d.* from (select * from employee where entrydate > '2006-01-01') as e left join dept as d on e.dept = d.id;
```

---

## 事务

事务是一组操作的集合，事务会把所有操作作为一个整体一起向系统提交或撤销操作请求，即这些操作要么同时成功，要么同时失败。

基本操作：

```sql
-- 1. 查询张三账户余额
select * from account where name = '张三';
-- 2. 将张三账户余额-1000
update account set money = money - 1000 where name = '张三';
-- 此语句出错后张三钱减少但是李四钱没有增加
模拟sql语句错误
-- 3. 将李四账户余额+1000
update account set money = money + 1000 where name = '李四';

-- 查看事务提交方式
SELECT @@AUTOCOMMIT;
-- 设置事务提交方式，1为自动提交，0为手动提交，该设置只对当前会话有效
SET @@AUTOCOMMIT = 0;
-- 提交事务
COMMIT;
-- 回滚事务
ROLLBACK;

-- 设置手动提交后上面代码改为：
select * from account where name = '张三';
update account set money = money - 1000 where name = '张三';
update account set money = money + 1000 where name = '李四';
commit;
```

操作方式二：

开启事务：  
`START TRANSACTION 或 BEGIN TRANSACTION;`  
提交事务：  
`COMMIT;`  
回滚事务：  
`ROLLBACK;`

操作实例：

```sql
start transaction;
select * from account where name = '张三';
update account set money = money - 1000 where name = '张三';
update account set money = money + 1000 where name = '李四';
commit;
```

### 四大特性ACID

- 原子性(Atomicity)：事务是不可分割的最小操作但愿，要么全部成功，要么全部失败
- 一致性(Consistency)：事务完成时，必须使所有数据都保持一致状态
- 隔离性(Isolation)：数据库系统提供的隔离机制，保证事务在不受外部并发操作影响的独立环境下运行
- 持久性(Durability)：事务一旦提交或回滚，它对数据库中的数据的改变就是永久的

## 并发控制(数据库系统概论)

事务可以一个一个地串行执行，即每个时刻只有一个事务运行。  
但为了充分利用系统资源，发挥数据库共享资源地特点，应允许多个事务并行地执行。  
在单处理机系统中，事务的并行执行实际上是这些并行事务的并行操作轮流交叉运行。称为**交叉并发方式**。虽然单处理机系统中的并行事务并没有真正地并行运行，但是减少了处理机待机的空闲时间，提高了系统的效率。  
在多处理机系统中，每个处理机都可以运行一个事务，实现多个事务真正的并行运行，称为**同时并发方式**。  

并发调度会出现一些问题：

|    问题    |     描述     |
| ---------- | ------------ |
|    脏读    | 一个事务读到另一个事务还没提交的数据  |
| 不可重复读  | 一个事务先后读取同一条记录，但两次读取的数据不同  |
|    幻读    | 一个事务按照条件查询数据时，没有对应的数据行，但是再插入数据时，又发现这行数据已经存在  |

> 这三个问题的详细演示：https://www.bilibili.com/video/BV1Kr4y1i7ru?p=55&vd_source=1a331f1dcf57697606b55b13be3078a0

### 封锁

封锁即事务在对某个数据对象例如表、记录等操作前，先向系统发出请求，对其加锁。加锁后此事务就对该数据对象有了一定的控制，在此事务释放它的锁之前，其他事务不能更新此数据对象。  

基本的封锁类型有两种：  
1. 排他锁(exclusive locks)，简称X锁，又称为写锁。  
	加锁后其他事务都不能再此对数据对象加任何类型的锁，即无法读取和修改。
2. 共享锁(share locks)，简称S锁。  
	加锁后，其他事务只能再对此数据对象加S锁，加锁的事务以及其他事务都只能读数据。

#### 封锁协议

封锁协议(locking protocol)指对何时申请什么锁、持锁时间、何时释放等规则的定义。

一级封锁协议:  

事务T在修改数据R之前必须先对其加X锁，直到事务结束才能释放。事务结束包括正常结束(commit)和非正常结束(rollback)。  
一级封锁协议可以防止丢失修改。

二级封锁协议:  

在一级封锁协议基础上增加事务T在读取数据R之前必须先对其加S锁，读完后即可释放S锁。  
进一步防止脏读。

三级封锁协议:  

在一级封锁协议的基础上增加事务T在读取数据R前必须先对其加S锁，直到事务结束才释放。  
进一步防止不可重复读。

#### 并发事务隔离级别

|      隔离级别     | 脏读 | 不可重复读 | 幻读 |
| ---------------- | ---- | --------- | ---- |
| Read uncommitted |   √  |     √     |   √  |
|  Read committed  |   ×  |     √     |   √  |
| Repeatable Read  |   ×  |     ×     |   √  |
|   Serializable   |   ×  |     ×     |   ×  |

- √表示在当前隔离级别下该问题会出现
- Serializable 性能最低；Read uncommitted 性能最高，数据安全性最差
- Repeatable Read为Mysql默认级别  

查看事务隔离级别：  
`SELECT @@TRANSACTION_ISOLATION;`  
设置事务隔离级别：  
`SET [ SESSION | GLOBAL ] TRANSACTION ISOLATION LEVEL {READ UNCOMMITTED | READ COMMITTED | REPEATABLE READ | SERIALIZABLE };`  
SESSION 是会话级别，表示只针对当前会话有效，GLOBAL 表示对所有会话有效

#### 死锁

一个事务T1封锁R1后请求封锁R2，但R2被事务T2封锁，T2又请求封锁R1，R1需要T1结束释放锁，T1又在等待T2结束释放锁。两事务无法结束，形成死锁。

目前解决死锁问题主要有两类方法: 预防与诊断。

预防：  
1. 一次封锁法：要求事务必须一次将所有要使用的数据全部加锁。  
	问题：  
	1. 全部加锁势必扩大了封锁的范围，从而降低了系统的并发度。
	2. 数据库的数据是不断变化的，原来不要求封锁的数据在执行过程中可能会变成封锁对象。所以难以精确地确定事务要封锁的数据对象，为此只能扩大封锁范围，进一步降低并发度。

2. 顺序封锁法：预先对数据对象规定一个封锁顺序，所有事务都按这个顺序实施封锁。  
	问题：  
	1. 数据随插入、删除不断变化，要维护这样的资源的封锁顺序非常困难，成本很高。
	2. 事务的封锁请求可以随着事务的执行二动态地决定，很难事先确定每一个事务要封锁哪些对象，因此难以按规定的顺序去施加封锁。

死锁的诊断与解除：  
1. 超时法：如果事务的等待时间超过了规定的时限，就认为发生了死锁。  
	问题：1. 误判	2. 设置时间太长就不能及时发现

2. 等待图法：用有向图表示事务的等待情况，周期性地进行死锁诊断。

解除：选择一个处理死锁代价最小的事务，将其撤销，释放此事务持有的所有的锁。被撤销的事务执行的数据修改会被恢复。

- 由于预防的难度，数据库普遍采用的是诊断并解除的方法。

### 可串行化调度

多个事务的并发执行是正确的，当且仅当其结果与按某一次序串行地执行这些事务时的结果相同，称这种调度策略为可串行化调度。  
可串行性是并发事务正确调度的准则。一个给定的并发调度，当且仅当它是可串行化的，才认为是正确调度。  

#### 冲突可串行化调度

冲突：指不同的事务对同一个数据的读写操作和写写操作。

一个调度 Sc 在保证冲突操作的次序不变的情况下，通过交换两个事务不冲突操作的次序得到另一个调度Sc'，如果Sc'是串行的，称调度Sc为**冲突可串行化**的调度。  

若一个调度是冲突可串行化，则一定是可串行化的调度。

### 两段锁协议

数据库普遍采用两段锁协议保证并发调度的正确性。

两段锁协议：  
	- 在对任何数据进行读写操作之前，首先要申请并获得对该数据的封锁。
	- 在释放一个封锁之后，事务不再申请和获得任何其他封锁。

所谓"两段"锁是指，事务分为两个阶段：  
第一阶段(扩展阶段)：获得封锁，事务可以申请获得任何数据项上的任何类型的锁，但是不能释放任何封锁。  
第二阶段(收缩阶段)：释放封锁，事务可以释放任何数据项上的任何类型的锁，但是不能再申请任何锁。

事务遵守两段锁协议是可串行化的调度的充分条件。

- 锁在Mysql中的应用详见[进阶篇-锁](##锁)

# 进阶篇

## 存储引擎

MySQL体系结构：

![结构图](https://dhc.pythonanywhere.com/media/editor/MySQL体系结构_20220315034329549927.png "结构图")
![层级描述](https://dhc.pythonanywhere.com/media/editor/MySQL体系结构层级含义_20220315034359342837.png "层级描述")

存储引擎就是存储数据、建立索引、更新/查询数据等技术的实现方式。存储引擎是基于表而不是基于库的，所以存储引擎也可以被称为表引擎。  
默认存储引擎是InnoDB。

相关操作：

```sql
-- 查询建表语句
show create table account;
-- 建表时指定存储引擎
CREATE TABLE 表名(
	...
) ENGINE=INNODB;
-- 查看当前数据库支持的存储引擎
show engines;
```

### InnoDB

InnoDB 是一种兼顾高可靠性和高性能的通用存储引擎，在 MySQL 5.5 之后，InnoDB 是默认的 MySQL 引擎。

特点：

- DML 操作遵循 ACID 模型，支持**事务**
- **行级锁**，提高并发访问性能
- 支持**外键**约束，保证数据的完整性和正确性

文件：

- xxx.ibd: xxx代表表名，InnoDB 引擎的每张表都会对应这样一个表空间文件，存储该表的表结构（frm、sdi）、数据和索引。

参数：innodb_file_per_table，决定多张表共享一个表空间还是每张表对应一个表空间

知识点：

查看 Mysql 变量：  
`show variables like 'innodb_file_per_table';`

从idb文件提取表结构数据：  
（在cmd运行）  
`ibd2sdi xxx.ibd`

InnoDB 逻辑存储结构：
![InnoDB逻辑存储结构](https://dhc.pythonanywhere.com/media/editor/逻辑存储结构_20220316030616590001.png "InnoDB逻辑存储结构")

### MyISAM

MyISAM 是 MySQL 早期的默认存储引擎。

特点：

- 不支持事务，不支持外键
- 支持表锁，不支持行锁
- 访问速度快

文件：

- xxx.sdi: 存储表结构信息
- xxx.MYD: 存储数据
- xxx.MYI: 存储索引

### Memory

Memory 引擎的表数据是存储在内存中的，受硬件问题、断电问题的影响，只能将这些表作为临时表或缓存使用。

特点：

- 存放在内存中，速度快
- hash索引（默认）

文件：

- xxx.sdi: 存储表结构信息

### 存储引擎特点

| 特点  | InnoDB  | MyISAM  | Memory  |
| ------------ | ------------ | ------------ | ------------ |
| 存储限制  | 64TB  | 有  | 有  |
| 事务安全  | 支持  | -  | -  |
| 锁机制  | 行锁  | 表锁  | 表锁  |
| B+tree索引  | 支持  | 支持  | 支持  |
| Hash索引  | -  | -  | 支持  |
| 全文索引  | 支持（5.6版本之后）  | 支持  | -  |
| 空间使用  | 高  | 低  | N/A  |
| 内存使用  | 高  | 低  | 中等  |
| 批量插入速度  | 低  | 高  | 高  |
| 支持外键  | 支持  | -  | -  |

### 存储引擎的选择

在选择存储引擎时，应该根据应用系统的特点选择合适的存储引擎。对于复杂的应用系统，还可以根据实际情况选择多种存储引擎进行组合。

- InnoDB: 如果应用对事物的完整性有比较高的要求，在并发条件下要求数据的一致性，数据操作除了插入和查询之外，还包含很多的更新、删除操作，则 InnoDB 是比较合适的选择
- MyISAM: 如果应用是以读操作和插入操作为主，只有很少的更新和删除操作，并且对事务的完整性、并发性要求不高，那这个存储引擎是非常合适的。
- Memory: 将所有数据保存在内存中，访问速度快，通常用于临时表及缓存。Memory 的缺陷是对表的大小有限制，太大的表无法缓存在内存中，而且无法保障数据的安全性

电商中的足迹和评论适合使用 MyISAM 引擎，缓存适合使用 Memory 引擎。

## 性能分析

### 查看执行频次

查看当前数据库的 INSERT, UPDATE, DELETE, SELECT 访问频次：  
`SHOW GLOBAL STATUS LIKE 'Com_______';` 或者 `SHOW SESSION STATUS LIKE 'Com_______';`  
例：`show global status like 'Com_______'`

### 慢查询日志

慢查询日志记录了所有执行时间超过指定参数（long_query_time，单位：秒，默认10秒）的所有SQL语句的日志。  
MySQL的慢查询日志默认没有开启，需要在MySQL的配置文件（/etc/my.cnf）中配置如下信息：
	# 开启慢查询日志开关
	slow_query_log=1
	# 设置慢查询日志的时间为2秒，SQL语句执行时间超过2秒，就会视为慢查询，记录慢查询日志
	long_query_time=2
更改后记得重启MySQL服务，日志文件位置：/var/lib/mysql/localhost-slow.log

查看慢查询日志开关状态：  
`show variables like 'slow_query_log';`

### profile

show profile 能在做SQL优化时帮我们了解时间都耗费在哪里。通过 have_profiling 参数，能看到当前 MySQL 是否支持 profile 操作：  
`SELECT @@have_profiling;`  
profiling 默认关闭，可以通过set语句在session/global级别开启 profiling：  
`SET profiling = 1;`  
查看所有语句的耗时：  
`show profiles;`  
查看指定query_id的SQL语句各个阶段的耗时：  
`show profile for query query_id;`  
查看指定query_id的SQL语句CPU的使用情况  
`show profile cpu for query query_id;`

### explain

EXPLAIN 或者 DESC 命令获取 MySQL 如何执行 SELECT 语句的信息，包括在 SELECT 语句执行过程中表如何连接和连接的顺序。  
语法：
	# 直接在select语句之前加上关键字 explain / desc
	EXPLAIN SELECT 字段列表 FROM 表名 HWERE 条件;

EXPLAIN 各字段含义：

- id：select 查询的序列号，表示查询中执行 select 子句或者操作表的顺序（id相同，执行顺序从上到下；id不同，值越大越先执行）
- select_type：表示 SELECT 的类型，常见取值有 SIMPLE（简单表，即不适用表连接或者子查询）、PRIMARY（主查询，即外层的查询）、UNION（UNION中的第二个或者后面的查询语句）、SUBQUERY（SELECT/WHERE之后包含了子查询）等
- type：表示连接类型，性能由好到差的连接类型为 NULL、system、const、eq_ref、ref、range、index、all
- possible_key：可能应用在这张表上的索引，一个或多个
- Key：实际使用的索引，如果为 NULL，则没有使用索引
- Key_len：表示索引中使用的字节数，该值为索引字段最大可能长度，并非实际使用长度，在不损失精确性的前提下，长度越短越好
- rows：MySQL认为必须要执行的行数，在InnoDB引擎的表中，是一个估计值，可能并不总是准确的
- filtered：表示返回结果的行数占需读取行数的百分比，filtered的值越大越好

## 索引

索引是帮助 MySQL **高效获取数据**的**数据结构（有序）**。在数据之外，数据库系统还维护着满足特定查找算法的数据结构，这些数据结构以某种方式引用（指向）数据，这样就可以在这些数据结构上实现高级查询算法，这种数据结构就是索引。

优缺点：

优点：

- 提高数据检索效率，降低数据库的IO成本
- 通过索引列对数据进行排序，降低数据排序的成本，降低CPU的消耗

缺点：

- 索引列也是要占用空间的
- 索引大大提高了查询效率，但降低了更新的速度，比如 INSERT、UPDATE、DELETE

### 索引结构

| 索引结构  | 描述  |
| ------------ | ------------ |
| B+Tree  | 最常见的索引类型，大部分引擎都支持B+树索引  |
| Hash  | 底层数据结构是用哈希表实现，只有精确匹配索引列的查询才有效，不支持范围查询  |
| R-Tree(空间索引)  | 空间索引是 MyISAM 引擎的一个特殊索引类型，主要用于地理空间数据类型，通常使用较少  |
| Full-Text(全文索引)  | 是一种通过建立倒排索引，快速匹配文档的方式，类似于 Lucene, Solr, ES  |

| 索引  | InnoDB  | MyISAM  | Memory  |
| ------------ | ------------ | ------------ | ------------ |
| B+Tree索引  | 支持  | 支持  | 支持  |
| Hash索引  | 不支持  | 不支持  | 支持  |
| R-Tree索引  | 不支持  | 支持  | 不支持  |
| Full-text  | 5.6版本后支持  | 支持  | 不支持  |

#### B-Tree

![二叉树](https://dhc.pythonanywhere.com/media/editor/二叉树_20220316153214227108.png "二叉树")

二叉树的缺点可以用红黑树来解决：
![红黑树](https://dhc.pythonanywhere.com/media/editor/红黑树_20220316163142686602.png "红黑树")
红黑树也存在大数据量情况下，层级较深，检索速度慢的问题。

为了解决上述问题，可以使用 B-Tree 结构。  
B-Tree (多路平衡查找树) 以一棵最大度数（max-degree，指一个节点的子节点个数）为5（5阶）的 b-tree 为例（每个节点最多存储4个key，5个指针）

![B-Tree结构](https://dhc.pythonanywhere.com/media/editor/B-Tree结构_20220316163813441163.png "B-Tree结构")

> B-Tree 的数据插入过程动画参照：https://www.bilibili.com/video/BV1Kr4y1i7ru?p=68
演示地址：https://www.cs.usfca.edu/~galles/visualization/BTree.html

#### B+Tree

结构图：

![B+Tree结构图](https://dhc.pythonanywhere.com/media/editor/B+Tree结构图_20220316170700591277.png "B+Tree结构图")

> 演示地址：https://www.cs.usfca.edu/~galles/visualization/BPlusTree.html

与 B-Tree 的区别：

- 所有的数据都会出现在叶子节点
- 叶子节点形成一个单向链表

MySQL 索引数据结构对经典的 B+Tree 进行了优化。在原 B+Tree 的基础上，增加一个指向相邻叶子节点的链表指针，就形成了带有顺序指针的 B+Tree，提高区间访问的性能。

![MySQL B+Tree 结构图](https://dhc.pythonanywhere.com/media/editor/结构图_20220316171730865611.png "MySQL B+Tree 结构图")

#### Hash

哈希索引就是采用一定的hash算法，将键值换算成新的hash值，映射到对应的槽位上，然后存储在hash表中。  
如果两个（或多个）键值，映射到一个相同的槽位上，他们就产生了hash冲突（也称为hash碰撞），可以通过链表来解决。

![Hash索引原理图](https://dhc.pythonanywhere.com/media/editor/Hash索引原理图_20220317143226150679.png "Hash索引原理图")

特点：

- Hash索引只能用于对等比较（=、in），不支持范围查询（betwwn、>、<、...）
- 无法利用索引完成排序操作
- 查询效率高，通常只需要一次检索就可以了，效率通常要高于 B+Tree 索引

存储引擎支持：

- Memory
- InnoDB: 具有自适应hash功能，hash索引是存储引擎根据 B+Tree 索引在指定条件下自动构建的

#### 面试题

1. 为什么 InnoDB 存储引擎选择使用 B+Tree 索引结构？

- 相对于二叉树，层级更少，搜索效率高
- 对于 B-Tree，无论是叶子节点还是非叶子节点，都会保存数据，这样导致一页中存储的键值减少，指针也跟着减少，要同样保存大量数据，只能增加树的高度，导致性能降低
- 相对于 Hash 索引，B+Tree 支持范围匹配及排序操作

### 索引分类

| 分类  | 含义  | 特点  | 关键字  |
| ------------ | ------------ | ------------ | ------------ |
| 主键索引  | 针对于表中主键创建的索引  | 默认自动创建，只能有一个  | PRIMARY  |
| 唯一索引  | 避免同一个表中某数据列中的值重复  | 可以有多个  | UNIQUE  |
| 常规索引  | 快速定位特定数据  | 可以有多个  |   |
| 全文索引  | 全文索引查找的是文本中的关键词，而不是比较索引中的值  | 可以有多个  | FULLTEXT  |

在 InnoDB 存储引擎中，根据索引的存储形式，又可以分为以下两种：

| 分类  | 含义  | 特点  |
| ------------ | ------------ | ------------ |
| 聚集索引(Clustered Index)  | 将数据存储与索引放一块，索引结构的叶子节点保存了行数据  | 必须有，而且只有一个  |
| 二级索引(Secondary Index)  | 将数据与索引分开存储，索引结构的叶子节点关联的是对应的主键  | 可以存在多个  |

演示图：

![大致原理](https://dhc.pythonanywhere.com/media/editor/原理图_20220318194454880073.png "大致原理")
![演示图](https://dhc.pythonanywhere.com/media/editor/演示图_20220319215403721066.png "演示图")

聚集索引选取规则：

- 如果存在主键，主键索引就是聚集索引
- 如果不存在主键，将使用第一个唯一(UNIQUE)索引作为聚集索引
- 如果表没有主键或没有合适的唯一索引，则 InnoDB 会自动生成一个 rowid 作为隐藏的聚集索引

#### 思考题

1\. 以下 SQL 语句，哪个执行效率高？为什么？

```sql
select * from user where id = 10;
select * from user where name = 'Arm';
-- 备注：id为主键，name字段创建的有索引
```

答：第一条语句，因为第二条需要回表查询，相当于两个步骤。

2\. InnoDB 主键索引的 B+Tree 高度为多少？

答：假设一行数据大小为1k，一页中可以存储16行这样的数据。InnoDB 的指针占用6个字节的空间，主键假设为bigint，占用字节数为8.  
可得公式：`n * 8 + (n + 1) * 6 = 16 * 1024`，其中 8 表示 bigint 占用的字节数，n 表示当前节点存储的key的数量，(n + 1) 表示指针数量（比key多一个）。算出n约为1170。

如果树的高度为2，那么他能存储的数据量大概为：`1171 * 16 = 18736`；  
如果树的高度为3，那么他能存储的数据量大概为：`1171 * 1171 * 16 = 21939856`。  

另外，如果有成千上万的数据，那么就要考虑分表，涉及运维篇知识。

### 语法

创建索引：  
`CREATE [ UNIQUE | FULLTEXT ] INDEX index_name ON table_name (index_col_name, ...);`  
如果不加 CREATE 后面不加索引类型参数，则创建的是常规索引

查看索引：  
`SHOW INDEX FROM table_name;`

删除索引：  
`DROP INDEX index_name ON table_name;`

案例：

```sql
-- name字段为姓名字段，该字段的值可能会重复，为该字段创建索引
create index idx_user_name on tb_user(name);
-- phone手机号字段的值非空，且唯一，为该字段创建唯一索引
create unique index idx_user_phone on tb_user (phone);
-- 为profession, age, status创建联合索引
create index idx_user_pro_age_stat on tb_user(profession, age, status);
-- 为email建立合适的索引来提升查询效率
create index idx_user_email on tb_user(email);

-- 删除索引
drop index idx_user_email on tb_user;
```

### 使用规则

#### 最左前缀法则

如果索引关联了多列（联合索引），要遵守最左前缀法则，最左前缀法则指的是查询从索引的最左列开始，并且不跳过索引中的列。  
如果跳跃某一列，索引将部分失效（后面的字段索引失效）。

联合索引中，出现范围查询（<, >），范围查询右侧的列索引失效。可以用>=或者<=来规避索引失效问题。

#### 索引失效情况

1. 在索引列上进行运算操作，索引将失效。如：`explain select * from tb_user where substring(phone, 10, 2) = '15';`
2. 字符串类型字段使用时，不加引号，索引将失效。如：`explain select * from tb_user where phone = 17799990015;`，此处phone的值没有加引号
3. 模糊查询中，如果仅仅是尾部模糊匹配，索引不会是失效；如果是头部模糊匹配，索引失效。如：`explain select * from tb_user where profession like '%工程';`，前后都有 % 也会失效。
4. 用 or 分割开的条件，如果 or 其中一个条件的列没有索引，那么涉及的索引都不会被用到。
5. 如果 MySQL 评估使用索引比全表更慢，则不使用索引。

#### SQL 提示

是优化数据库的一个重要手段，简单来说，就是在SQL语句中加入一些人为的提示来达到优化操作的目的。

例如，使用索引：  
`explain select * from tb_user use index(idx_user_pro) where profession="软件工程";`
不使用哪个索引：  
`explain select * from tb_user ignore index(idx_user_pro) where profession="软件工程";`
必须使用哪个索引：  
`explain select * from tb_user force index(idx_user_pro) where profession="软件工程";`

use 是建议，实际使用哪个索引 MySQL 还会自己权衡运行速度去更改，force就是无论如何都强制使用该索引。

#### 覆盖索引&回表查询

尽量使用覆盖索引（查询使用了索引，并且需要返回的列，在该索引中已经全部能找到），减少 select *。

explain 中 extra 字段含义：  
`using index condition`：查找使用了索引，但是需要回表查询数据.  
`using where; using index;`：查找使用了索引，但是需要的数据都在索引列中能找到，所以不需要回表查询.  

如果在聚集索引中直接能找到对应的行，则直接返回行数据，只需要一次查询，哪怕是select \*；如果在辅助索引中找聚集索引，如`select id, name from xxx where name='xxx';`，也只需要通过辅助索引(name)查找到对应的id，返回name和name索引对应的id即可，只需要一次查询；如果是通过辅助索引查找其他字段，则需要回表查询，如`select id, name, gender from xxx where name='xxx';`

所以尽量不要用`select *`，容易出现回表查询，降低效率，除非有联合索引包含了所有字段

面试题：一张表，有四个字段（id, username, password, status），由于数据量大，需要对以下SQL语句进行优化，该如何进行才是最优方案：  
`select id, username, password from tb_user where username='itcast';`

解：给username和password字段建立联合索引，则不需要回表查询，直接覆盖索引

#### 前缀索引

当字段类型为字符串（varchar, text等）时，有时候需要索引很长的字符串，这会让索引变得很大，查询时，浪费大量的磁盘IO，影响查询效率，此时可以只降字符串的一部分前缀，建立索引，这样可以大大节约索引空间，从而提高索引效率。

语法：`create index idx_xxxx on table_name(columnn(n));`  
前缀长度：可以根据索引的选择性来决定，而选择性是指不重复的索引值（基数）和数据表的记录总数的比值，索引选择性越高则查询效率越高，唯一索引的选择性是1，这是最好的索引选择性，性能也是最好的。  
求选择性公式：
```sql
select count(distinct email) / count(*) from tb_user;
select count(distinct substring(email, 1, 5)) / count(*) from tb_user;
```

show index 里面的sub_part可以看到接取的长度

#### 单列索引&联合索引

单列索引：即一个索引只包含单个列  
联合索引：即一个索引包含了多个列  
在业务场景中，如果存在多个查询条件，考虑针对于查询字段建立索引时，建议建立联合索引，而非单列索引。

单列索引情况：  
`explain select id, phone, name from tb_user where phone = '17799990010' and name = '韩信';`  
这句只会用到phone索引字段

##### 注意事项

- 多条件联合查询时，MySQL优化器会评估哪个字段的索引效率更高，会选择该索引完成本次查询

### 设计原则

1. 针对于数据量较大，且查询比较频繁的表建立索引
2. 针对于常作为查询条件（where）、排序（order by）、分组（group by）操作的字段建立索引
3. 尽量选择区分度高的列作为索引，尽量建立唯一索引，区分度越高，使用索引的效率越高
4. 如果是字符串类型的字段，字段长度较长，可以针对于字段的特点，建立前缀索引
5. 尽量使用联合索引，减少单列索引，查询时，联合索引很多时候可以覆盖索引，节省存储空间，避免回表，提高查询效率
6. 要控制索引的数量，索引并不是多多益善，索引越多，维护索引结构的代价就越大，会影响增删改的效率
7. 如果索引列不能存储NULL值，请在创建表时使用NOT NULL约束它。当优化器知道每列是否包含NULL值时，它可以更好地确定哪个索引最有效地用于查询

## SQL 优化

### 插入数据

普通插入：

1. 采用批量插入（一次插入的数据不建议超过1000条）
2. 手动提交事务
3. 主键顺序插入

大批量插入：  
如果一次性需要插入大批量数据，使用insert语句插入性能较低，此时可以使用MySQL数据库提供的load指令插入。

```sql
-- 客户端连接服务端时，加上参数 --local-infile（这一行在bash/cmd界面输入）
-- mysql --local-infile -u root -p

-- 设置全局参数local_infile为1，开启从本地加载文件导入数据的开关
set global local_infile = 1;
select @@local_infile;
-- 执行load指令将准备好的数据，加载到表结构中
load data local infile '/root/sql1.log' into table 'tb_user' fields terminated by ',' lines terminated by '\n';
```

### 主键优化

数据组织方式：在InnoDB存储引擎中，表数据都是根据主键顺序组织存放的，这种存储方式的表称为索引组织表（Index organized table, IOT）

页分裂：页可以为空，也可以填充一般，也可以填充100%，每个页包含了2-N行数据（如果一行数据过大，会行溢出），根据主键排列。  
页合并：当删除一行记录时，实际上记录并没有被物理删除，只是记录被标记（flaged）为删除并且它的空间变得允许被其他记录声明使用。当页中删除的记录到达 MERGE_THRESHOLD（默认为页的50%），InnoDB会开始寻找最靠近的页（前后）看看是否可以将这两个页合并以优化空间使用。

MERGE_THRESHOLD：合并页的阈值，可以自己设置，在创建表或创建索引时指定

> 文字说明不够清晰明了，具体可以看视频里的PPT演示过程：https://www.bilibili.com/video/BV1Kr4y1i7ru?p=90

主键设计原则：

- 满足业务需求的情况下，尽量降低主键的长度
- 插入数据时，尽量选择顺序插入，选择使用 AUTO_INCREMENT 自增主键
- 尽量不要使用 UUID 做主键或者是其他的自然主键，如身份证号
- 业务操作时，避免对主键的修改

### order by优化

1. Using filesort：通过表的索引或全表扫描，读取满足条件的数据行，然后在排序缓冲区 sort buffer 中完成排序操作，所有不是通过索引直接返回排序结果的排序都叫 FileSort 排序
2. Using index：通过有序索引顺序扫描直接返回有序数据，这种情况即为 using index，不需要额外排序，操作效率高

如果order by字段全部使用升序排序或者降序排序，则都会走索引，但是如果一个字段升序排序，另一个字段降序排序，则不会走索引，explain的extra信息显示的是`Using index, Using filesort`，如果要优化掉Using filesort，则需要另外再创建一个索引，如：`create index idx_user_age_phone_ad on tb_user(age asc, phone desc);`，此时使用`select id, age, phone from tb_user order by age asc, phone desc;`会全部走索引

总结：

- 根据排序字段建立合适的索引，多字段排序时，也遵循最左前缀法则
- 尽量使用覆盖索引
- 多字段排序，一个升序一个降序，此时需要注意联合索引在创建时的规则（ASC/DESC）
- 如果不可避免出现filesort，大数据量排序时，可以适当增大排序缓冲区大小 sort_buffer_size（默认256k）

### group by优化

- 在分组操作时，可以通过索引来提高效率
- 分组操作时，索引的使用也是满足最左前缀法则的

如索引为`idx_user_pro_age_stat`，则句式可以是`select ... where profession order by age`，这样也符合最左前缀法则

### limit优化

常见的问题如`limit 2000000, 10`，此时需要 MySQL 排序前2000000条记录，但仅仅返回2000000 - 2000010的记录，其他记录丢弃，查询排序的代价非常大。  
优化方案：一般分页查询时，通过创建覆盖索引能够比较好地提高性能，可以通过覆盖索引加子查询形式进行优化

例如：

```sql
-- 此语句耗时很长
select * from tb_sku limit 9000000, 10;
-- 通过覆盖索引加快速度，直接通过主键索引进行排序及查询
select id from tb_sku order by id limit 9000000, 10;
-- 下面的语句是错误的，因为 MySQL 不支持 in 里面使用 limit
-- select * from tb_sku where id in (select id from tb_sku order by id limit 9000000, 10);
-- 通过连表查询即可实现第一句的效果，并且能达到第二句的速度
select * from tb_sku as s, (select id from tb_sku order by id limit 9000000, 10) as a where s.id = a.id;
```

### count优化

MyISAM 引擎把一个表的总行数存在了磁盘上，因此执行 count(\*) 的时候会直接返回这个数，效率很高（前提是不适用where）;  
InnoDB 在执行 count(\*) 时，需要把数据一行一行地从引擎里面读出来，然后累计计数。  
优化方案：自己计数，如创建key-value表存储在内存或硬盘，或者是用redis

count的几种用法：

- 如果count函数的参数（count里面写的那个字段）不是NULL（字段值不为NULL），累计值就加一，最后返回累计值
- 用法：count(\*)、count(主键)、count(字段)、count(1)
- count(主键)跟count(\*)一样，因为主键不能为空；count(字段)只计算字段值不为NULL的行；count(1)引擎会为每行添加一个1，然后就count这个1，返回结果也跟count(\*)一样；count(null)返回0

各种用法的性能：

- count(主键)：InnoDB引擎会遍历整张表，把每行的主键id值都取出来，返回给服务层，服务层拿到主键后，直接按行进行累加（主键不可能为空）
- count(字段)：没有not null约束的话，InnoDB引擎会遍历整张表把每一行的字段值都取出来，返回给服务层，服务层判断是否为null，不为null，计数累加；有not null约束的话，InnoDB引擎会遍历整张表把每一行的字段值都取出来，返回给服务层，直接按行进行累加
- count(1)：InnoDB 引擎遍历整张表，但不取值。服务层对于返回的每一层，放一个数字 1 进去，直接按行进行累加
- count(\*)：InnoDB 引擎并不会把全部字段取出来，而是专门做了优化，不取值，服务层直接按行进行累加

按效率排序：count(字段) < count(主键) < count(1) < count(\*)，所以尽量使用 count(\*)

### update优化（避免行锁升级为表锁）

InnoDB 的行锁是针对索引加的锁，不是针对记录加的锁，并且该索引不能失效，否则会从行锁升级为表锁。

如以下两条语句：  
`update student set no = '123' where id = 1;`，这句由于id有主键索引，所以只会锁这一行；  
`update student set no = '123' where name = 'test';`，这句由于name没有索引，所以会把整张表都锁住进行数据更新，解决方法是给name字段添加索引

## 视图
### 介绍

视图为一种虚拟存在的表。视图建立在其它的表之上，其数据来自其他表中。视图只是保存了查询的SQL逻辑，不保存结果。视图是表的一个窗口。

### 语法

创建:  
`create [or replace] view view_name [列名列表] as <子查询> [with [cascaded|local] check option]`  
- 对视图的数据更改会反映在基本表中,未指定的列数据默认为null.
- check option: 阻止插入超过视图范围的数据,即满足子查询的条件.
- MySQL允许基于一个视图创建视图.  
	- cascaded(默认): 在视图中的增删改会检查是否符合所有上级视图的条件,**即使没有添加check选项**.  
	- local: 只检查此视图的条件,以及上级中**添加了check选项的条件**.
- 不是所有的视图都可以更新,比如带有聚合函数的视图,只有视图中的一行对应表中一行数据时可更新.  

查询:  
`show create view view_name` -- 查询指定视图的信息  
`select * from view_name` --视图完全可以当表使用 

修改:  
1. 再创建一个同名视图,原视图会被覆盖.
2. `alter view view_name [列名列表] as select语句 [with[cascaded|local] check option]`

删除:  
`drop view [if exists] view_name`

### 作用

1. 简化查询: 将复杂的查询定义为视图,直接查询视图即可.
2. 安全性: 通过视图来控制不同用户权限对表的查询以及修改.
3. 数据独立: 帮用户屏蔽真实表结构变化带来的影响.

## 存储过程

存储过程是事先经过编译并存储在数据库中的一段SQL语句的集合, 调用存储过程可以简化应用开发人员的很多工作, 减少数据在数据库和应用服务器之间的传输, 对于提高数据处理的效率是有好处的。  
存储过程即数据库SQL语言层面的代码封装与重用。 

### 基本语法

- 创建：  
```sql
creat procedure <pro_name>([参数列表])
begin
	SQL语句
end;
```
创建的存储过程会自动保持在routines文件夹中  
在命令行创建存储过程时内容中SQL语句的“ ; ”会让创建语句提前结束而报错, 可以通过 `delimiter <任意单个或多个符号> 指定命令行的语句结束符号, 再将end后的" ; "替换为设置的符号即可。

- 调用：`call <pro_name>([参数]);`

- 查看：  
查看指定数据库的存储过程及状态信息  
`select * from information_schema.routines where routine_schema='xxx';`  
查看某个存储过程的定义：  
`show create procedure <pro_name>;`

- 删除： `drop procedure [if exists] <pro_name>;`

### 系统变量

由Mysql服务器提供，分为全局变量(GLOBAL), 会话变量(SESSION).

- 查看系统变量  
查看所有系统变量: `show [session|global] variables;`  
模糊匹配查找变量: `show [session|global] variables like '...';`  
查看指定变量的值: `show @@[session|global] <系统变量名>;`  

- 设置系统变量  
`set [@@][session|global] <系统变量名> = <值>;`  

### 用户定义变量

用户变量不用提前声明, 通过 @<变量名> 使用  

- 赋值  
`set @<变量名> [:]= ...;`  
`select @<变量名> [:]= ...;`  
`select count(*) into @<变量名> ...;`  

- 查询  
`select @<变量名>, @<变量名>, ...`

### 局部变量

局部变量是根据需要定义的在局部生效的变量, 访问之前, 需要declear声明。可用作存储过程内的局部变量和输入参数，局部变量的范围是在其声明的Begin...End块。

- 声明：`DECLEAR 变量名 变量类型 [default]`  
- 赋值：set 或 select ... into 变量名 from ...

### if判断
```
if ... then

elseif ... then

else

end if;
```

### 参数

| 类型 | 含义 |
| --- | --- |
| in(默认) | 该类参数作为输入，也就是需要调用时传入值 |
| out | 该类参数作为输出，也就是该参数可以作为返回值 |
| inout | 既可以作为输入参数，也可以作为输出参数 |

`create procedure p_name([in/out/inout 参数名 参数类型])`  
`call p_name([传入参数], [@返回值])`  

### case

语法:  
1.   
```sql
-- case_value为需要判断的变量, value1等为可能的值.

case case_value
	when when_value1 then statement_list1
	[when when_value2 then statement_list2]...
	[else statement_list]
end case;
```
2.  
```sql
-- condition1等为判断条件

case
	when search_condition1 then statement_list1
	[when search_condition2 then statement_list2]...
	[else statement_list]
end case;
```

例子:  
```SQL
-- 根据输入的月份判断其所属的季度

create procedure p(in month int)
begin
	declare result varchar(10);

	case
		when month >= 1 and month <= 3 then
			set result := '第一季度';
		when month >= 4 and month <= 6 then
			set result := '第二季度';
		when month >= 7 and month <= 9 then
			set result := '第三季度';
		when month >= 10 and month <= 12 then
			set result := '第四季度';
		else
			set result := '非法参数';
	end case;

	select concat('您输入的月份为: ',month, ', 所属的季度为: ',result);
end;

call p(6);
```

### 循环

- while:  
	```
	while 条件 do
		循环体...
	end while
	```

- repeat:  
	```
	# 条件为退出循环的条件, 且循环体至少会执行一次
	repeat
		循环体...
		until 条件
	end repeat;
	```

- loop:  
	```
	-- loop循环中有两个配套的关键字
	-- leave: 退出循环, (break)
	-- iterate: 直接进行下一次循环, (continue)

	[label:] loop
		循环体...
	end loop [label];

	-- label相当于循环的名字, leave与iterate 后可跟上 label 明确是哪个循环
	```

### 游标

游标(cursor)是用来存储查询结果集的数据类型, 在存储过程和函数中可以使用游标对结果集进行循环的处理.  
相当于一个数组用来存储查询得到的数据记录(元组).  

声明(游标的声明需要在一般变量之后):  
`declare 游标名称 cursor for 查询语句;`

打开游标:  
`open 游标名称;`

获取游标记录(配合循环):  
`fetch 游标名称 into 变量[, 变量...];`

关闭游标:  
`close 游标名称;`

条件处理程序(handler)  

条件处理程序可以用来定义在流程控制结构执行过程中遇到问题时相应的处理步骤.  
类似自定义的异常处理.  


`declare handler_action handler for condition_value [, condition_value]... statement;`

- handler_action:  
	continue: 继续执行当前程序  
	exit: 终止执行当前程序  
- continue_value:  
	sqlstate sqlstate_value: 状态码, 如02000  
	sqlwarning: 所有以01开头的sqlstate代码的简写  
	not found: 所有以02开头的sqlstate代码的简写  
	sqlexception: 所有没有被sqlwarning或not found捕获的sqlstate代码的简写  

例子(异常时终止执行并关闭游标):  
`declare exit handler for sqlstate '02000' close u_cursor`

[状态码官方文档](https://dev.mysql.com/doc/mysql-errors/8.0/en/server-error-reference.html)

### 存储函数

存储函数时有返回值的存储过程, 存储函数的参数只能是in类型.  

```sql
create function 存储函数名称([参数列表])
returns type [characteristic ...]
begin
	...
	return ...;
end;
```
返回值需要加上一些特征标签:  
- characteristic:  
	- deterministic: 相同的输入参数总是产生相同的结果.
	- no sql: 不包含sql语句.
	- reads sql data: 包含读取数据的语句, 但不包含写入数据的语句.  

存储函数一般都可以用存储过程代替, 所以较少使用.  

## 触发器

### 介绍

触发器是与表有关的数据库对象,在 **insert/update/delete** 之前或之后,触发并执行定义的SQL语句集合。触发器的这种特性可以协助应用在数据库端确保数据的完整性,日志记录,数据校验等操作。  

使用别名OLD和NEW来引用触发器中发生变化的记录内容,目前(2022)触发器还只支持行级触发(一次只更新一行数据),不支持语句级触发(特点语句即可触发,无论多少行)。  

old指**更新/删除**之前的数据,new为**更新/插入**之后的数据.

### 类型
- insert型触发器
- update型触发器
- delete型触发器

### 语法
创建
```sql
create trigger <tigger_name>  
before/after insert/update/delete  
on <table_name> for each row  
begin  
	[if(...)]
	[then] <执行的语句>
	[end if];  
end;
```
查看  
`show triggers;`

删除  
`drop tigger [schema_name.]tigger_name; --如果没有指定schema_name,则默认当前数据库.`  

示例:  
```sql
-- 在tb_user表中插入数据后在user_logs中插入相关日志信息
create trigger tb_user_insert_tigger
	after insert on tb_user for each row
begin
	insert into user_logs(id, operation, operate_time, operate_id, operate_params)  
	values (null, 'insert', now(), new.id, concat('插入的数据内容为:id=', new.id, ',name=', new.name,...));
end;
```

## 锁

锁是计算机协调多个进程或线程并发访问莫伊资源的机制。在数据库中，除传统的计算机资源(CPU、RAM、I/O)的争用以外，数据也是一种供许多用户共享的资源。如何**保证数据并发访问的一致性、有效性**是所有数据库必须解决的一个问题，锁冲突也是影响数据库并发访问性能的一个重要因素。从这个角度来说，锁对数据库而言显得尤其重要，也更加复杂。

按照锁的粒度分类:  
- 全局锁: 锁定数据库中的所有表.  
- 表级锁: 每次操作锁住整张表.  
- 行级锁: 每次操作锁住对应的行数据.  

参考上文理论部分 [并发控制-封锁](###封锁)

### 全局锁

全局锁就是对整个数据库实例加锁，加锁后整个实例就处于只读状态，后续的DML的写语句，DDL语句，以及更新操作的事务提交语句都将被阻塞。  
其典型的使用场景是做全库的逻辑备份，对所有的表进行锁定，从而获取一致性视图，保证数据的完整性。  

加锁：`flush tables with read lock;`  
解锁：`unlock tables;`  

### 表级锁

表级锁，每次操作锁住整张表。锁定粒度大，发生锁冲突的概率最高，并发度最低。应用在MyISAM、InnoDB、BDB中。  

表级锁主要分为以下三类：  
1. 表锁
2. 元数据锁(mate data lock MDL)
3. 意向锁

#### 表锁

语法:  
- 加锁: `lock tables table_name read/write`
- 释放: `unlock tables` 或者客户端断开连接

#### 元数据锁

MDL加锁过程是系统自动控制，无需显示使用，在访问一张表的时候会自动加上。MDL锁主要作用是维护表元数据的数据一致性，在表上有活动事务的时候，不可以对元数据进行写入操作。为了避免DML与DDL冲突，保证读写的正确性。

在MySQL5.5中引入了MDL，当对一张表进行增删改查的时候，加MDL读锁；当对表结构进行变更操作的时候，加MDL写锁。

元数据锁中的读锁与写锁相互兼容，都为共享锁(shared_read、shared_write)，更改表结构时加排他锁(exclusive)与共享锁互斥。

查看元数据锁：  
`select object_type,object_schema,object_name,lock_type,lock_duration from performance_schema.metadata_locks;`

#### 意向锁

为了避免DML在执行时, 加的行锁与表锁冲突, 在InnoDB中引入了意向锁, 使得表锁不用检查每行数据是否加了锁, 使用意向锁来减少表锁的检查.  

行锁施加时会同时对表加上意向锁, 另一事务加表锁时直接检查其意向锁与要加的锁是否兼容.  
查询语句会加上意向共享锁(IS), 增删改语句会加上排他锁(IX).  

查看意向锁及行锁的加锁情况:  
`select object_schema,object_name,index_name,lock_type,lock_mode,lock_data from performance_schema.data_locks;`  

### 行级锁

行级锁, 每次操作锁住对应的行数据. 锁定粒度最小, 发生锁冲突的概率最低, 并发度最高. 应用在InnoDB存储引擎中.  

InnoDB的数据是基于索引组织的, 行锁是通过对索引上的索引项加锁来实现的, 而不是对记录加的锁. 即锁的是主键, 而不是记录. 因为二级索引其叶子节点的数据是主键值而不是记录.  

行级锁分一下三类:  
1. 行锁(recode lock): 锁定单个行记录的锁, 防止其他事务的更新与删除. 在RC, RR隔离级别下都支持.   
2. 间隙锁(Gap Lock): 锁定索引记录的间隙(不含该记录), 确保索引记录间隙不变, 防止其他事务在这个间隙进行insert, 产生幻读. 在RR隔离级别支持.  
3. 临键锁(Next-Key Lock): 行锁与间隙锁的组合, 同时锁住数据与数据之间的间隙. 在RR隔离级别下支持.  

[并发事务隔离级别](####并发事务隔离级别)

#### 行锁

增删改会自动加排他锁, 一般select不会加任何锁.  

手动加锁:  
- 共享锁: 在select语句之后加上 `lock in share mode`.  
- 排他锁: 在select语句之后加上 `for update`.  

InnoDB在RR事务隔离级别下, 使用 next-key锁进行搜索和索引扫描, 以防止幻读.  
- 针对唯一索引进行检索时, 对已存在的记录进行等值匹配时, 将会自动优化为行锁.  
- InnoDB的行锁是针对索引加的锁, 不通过索引条件检索数据, 那么InnoDB将对表中的所有记录加锁, 此时就会升级为表锁.  

#### 间隙锁/临键锁

InnoDB在RR隔离级别时使用next-key锁进行搜索和索引扫描, 以防止幻读.  

1. 索引上的等值查询(唯一索引), 给不存在的记录加锁时, 优化为间隙锁.  
2. 索引上的等值查询(普通索引), 向右遍历时最后一个值不满足查询需求时, next-key lock 退化为间隙锁.  
3. 索引上的范围查询(唯一索引)--会访问到不满足条件的第一个值为止.  

- 注意: 间隙锁唯一目的是防止其他事务将数据插入间隙. 间隙锁可以共存, 一个事务采用的间隙锁不会阻止另一个事务在同一间隙上采用间隙锁.  

解释(可能有误):  
1. 一张表中根据主键id建立索引(自动建立), 已有的id={1, 3, 8, 11, 19, 15}.  
此时更新id = 5 的记录, id不存在, 会添加间隙锁, 锁定id为 3-8(不包括3和8) 之间的数据, 防止有数据插入其间造成幻读.  
2. 如果并非唯一索引, 会用间隙锁将所有等值的数据及其之间的间隙, 包括前一个与后一个数据之间的间隙锁定. 例如 {1, 3, 6, 6, 6, 9, 14}, 查询 6 时会锁住所有 3-9 之间的间隙.  

## InnoDB引擎

### 逻辑存储结构

一张表空间(Tablespace)中有多个段(Segment), 一个段中有多个区(Extent), 一个区有多个页(Page), 一页有多行(Row).  
表 -> 段 -> 区 -> 页 -> 行  

- 表空间: 对应一个ibd文件, 一个mysql实例可以对应多个表空间, 用于存储记录、索引等数据。  
- 段：分为数据段、索引段、回滚段。InnoDB是索引组织表，数据段就是B+树的叶子节点，索引段即为B+树的非叶子节点。段用来管理多个区。
- 区：表空间的单元结构，每个区的大小为 1M。默认情况下，InnoDB存储引擎页大小为16k，即一个区中一共有64个连续的页。  
- 页：是InnoDB存储引擎磁盘管理的最小单元，每个页默认16KB。为了保证页的连续性，InnoDB每次从磁盘申请4-5个区。
- 行：InnoDB数据是按行进行存放的。其中另记录了Trx_id(每次对某条记录进行改动时，都会把对应的事务id赋给trx_id隐藏列)，Roll_pointer(每次对某条记录进行改动时, 都会把旧的版本写入到undo日志中. 这个隐藏列相当于一个指针,通过它来找到该记录修改前的信息)

### 架构

MySQL5.5版本开始, 默认使用InnoDB存储引擎, 它擅长事务处理, 具有崩溃恢复特性, 在日常开发中使用非常广泛.  

#### 内存架构

- Buffer Pool:  
	缓冲池是主内存中的一个区域, 里面可以缓存磁盘上经常操作的真实数据, 在执行增删改查操作时, 先操作缓冲池中的数据(若缓冲池没有数据, 则从磁盘加载并缓存), 然后再以一定频率刷新到磁盘, 从而减少磁盘IO, 加快处理速度.  

	缓冲池以Page为单位, 底层采用链表数据结构管理Page. 根据状态, 将Page分为三种类型:  
	- free page: 空闲的page, 未被使用.  
	- clean page: 被使用page, 数据没有被修改过.  
	- dirty page: 脏页, 被使用page, 数据被修改过, 页中数据与磁盘的数据不一致.  

- Change Buffer:  
	更改缓冲区(针对于非唯一 二级索引页), 在执行DML语句时, 如果这些数据页不在Buffer Pool中, 不会直接操作磁盘, 而会将数据变更存在更改缓冲区 Change Buffer 中, 在未来数据被读取时, 在将数据合并恢复到Buffer Pool中, 再将合并后的数据刷新到磁盘中.  

	Change Buffer的意义:  
	与聚集索引不同, 二级索引通常是非唯一的, 并且以相对随机的顺序插入二级索引. 同样, 删除和更新可能会影响索引树中不相邻的二级索引页, 如果每一次都操作磁盘, 会造成大量的磁盘IO.  有了Change Buffer之后, 我们就可以在缓冲池中进行合并处理, 减少磁盘IO.  

- Adaptive Hash Index:  
	自适应hash索引, 用于优化对Buffer Pool数据的查询. InnoDB存储引擎会监控对表上各索引页的查询, 如果观察到hash索引可以提升速度, 则建立hash索引, 称之为自适应hash索引.  

- Log Buffer:  
	日志缓冲区, 用来保存要写入到磁盘中的log日志数据(redo log, undo log), 默认大小为16MB, 日志缓冲区的日志会定期刷新到磁盘中. 如果需要更新、插入或删除许多行的事务，增加日志缓冲区的大小可以节省磁盘IO。  
	参数变量：innodb_log_buffer_size(缓冲区大小), innodb_flush_log_at_trx_commit(日志刷新到磁盘时机, 0:每秒将日志写入并刷新到磁盘一次, 1:在每次事务提交时写入并刷新到磁盘, 2:每次事务提交后写入, 并每秒刷新到磁盘一次)

#### 磁盘结构

- System Tablespace:  
	系统表空间是更改缓冲区的存储区域。如果表是在系统表空间而不是每个表文件或通用表空间中创建的，它也可能包含表和索引数据。(在MySQL5.x版本还包含InnoDB数据字典, undolog等).

- File-Per-Table Tablespace:  
	每个表的文件表空间包含单个InnoDB表的数据和索引, 并存储在文件系统上的单个数据文件中(.idb文件即表空间文件).

- General Tablespace:  
	通用表空间,需要通过 `creat tablespace` 语法创建通用表空间, 在创建表时, 可以指定该表空间.  
	`create Tablespace ts_name add datafile 'file_name(.idb)' engine = 'engine_name';`  
	`create table table_name ... tablespace ts_name`  

- Undo Tablespace:  
	撤销表空间, MySQL实例在初始化时会自动创建两个默认的undo表空间(初始大小16M), 用于存储 undo log 日志.

- Temporary Tablespace:  
	InnoDB使用会话临时表空间和全局临时表空间. 存储用户创建的临时表等数据.  

- Doublewrite Buffer Files:  
	双写缓冲区, InnoDB引擎将数据页从Buffer Pool刷新到磁盘前, 先将数据页写入双写缓冲区文件中, 便于系统异常时恢复数据.  

- Redo Log:  
	重做日志, 是用来实现事务的持久性. 该日志文件由两部分组成: 重做日志缓冲(redo log buffer)以及重做日志文件(redo log), 前者是在内存中, 后者在磁盘中. 当事务提交之后会把所有修改信息都会存到该日志中, 用于在刷新脏页到磁盘时, 发生错误时, 进行数据恢复使用.  

#### 后台线程

1. Master Thread  
	核心后台线程, 负责调度其他线程, 还负责将缓冲池中的数据异步刷新到磁盘中, 保持数据的一致性, 还包括脏页的刷新, 合并插入缓存, undo页回收.  

2. IO Thread  
	在InnoDB存储引擎中大量使用了AIO(异步非阻塞IO)来处理IO请求, 这样可以极大地提高数据库地性能, 而IO Thread主要负责这些IO请求的回调.  
	| 线程类型             | 默认个数 | 职责      |
	| -------             | ------- | ----      |
	| Read thread         |  4      | 负责读操作 |
	| Write thread        |  4      | 负责写操作 |
	| Log thread          |  1      | 负责将日志缓冲区刷新到磁盘 |
	| Insert buffer thread |  1      | 负责将写缓冲区内容刷新到磁盘 |

3. Purge Thread  
	主要用于回收事务已提交了的undo log, 在事务提交之后, undo log可能不用了, 就用它来回收.  

4. Page Cleaner Thread  
	协助 Master Thread 刷新脏页到磁盘的线程, 它可以减轻 Master Thread 的工作压力, 减少阻塞.  

### 事务原理

实现支持事务的关键为满足事务的四大特性: 原子性, 一致性, 隔离性, 持久性.  

原子性, 一致性, 持久性 通过 redo log 与 undo log 日志实现, 隔离性通过 锁 与 MVCC 实现.  

#### redo log

重做日志, 记录的是事务提交时数据页的物理修改, 是用来实现事务的持久性.  
该日志文件由两部分组成: 重做日志缓冲(redo log buffer) 以及 重做日志文件(redo log file), 前者在内存中, 后者在磁盘中. 当事务提交之后会把所有的修改信息都存到该日志文件中, 用于在刷新脏页到磁盘发生错误时进行数据恢复使用.  

详细说明:  
在变更数据时先写入内存中, 并记录此次变更到 redo log buffer 且之间将buffer写入磁盘. 因为数据变更是随机写入, 性能较慢, 而redo log为顺序写入. 之后通过后台线程将脏页(变更数据)写入磁盘. 如果写入时发生错误也可以通过redo log恢复.   

#### undo log

回滚日志, 用于记录数据被修改前的信息, 作用: 提供回滚 和 MVCC(多版本并发控制).  
undo log 和 redo log 记录物理日志不同, 它是逻辑日志. 可以认为当delete一条记录时, undo log中会记录一条对应的insert记录, 反之亦然, 当update一条记录时, 它记录一条对应相反的update记录. 当执行rollback时, 就可以从undo log中的逻辑记录读取到相应的内容并进行回滚.  

undo log销毁: undo在事务执行时产生, 事务提交时, 并不会立即删除undo log, 因为这些日志可能还用于MVCC.  
undo log存储: undo log采用段的方式进行管理和记录, 存放在上文介绍的 rollback segment 回滚段中, 内部包含1024个undo log segment.  

### MVCC

#### 概念

- 当前读:  
	读取的是记录的最新版本, 读取时还要保证其他并发事务不能修改当前记录, 会对读取的记录进行加锁. 对于我们的日常操作, 如: select ... lock in share mode, select ... for update, update, insert, delete 都是一种当前读.  

- 快照读:  
	简单的select(不加锁)就是快照读, 读取的是记录数据的可见版本, 有可能是历史数据, 不加锁, 是非阻塞读. (即在select之后其他事务更新了数据也不会被重新读取)  
	- Read Committed: 每次select, 都生成一个快照读.  
	- Repeatable Read: 开启事务后第一个select语句才是快照读的地方.  
	- Serializable: 快照读会退化为当前读.  

- MVCC:  
	Multi-Version Concurrency Control, 多版本并发控制. 指维护一个数据的多个版本, 使得读写操作没有冲突, 快照读为MySQL实现MVCC提供了一个非阻塞读写功能. MVCC的具体实现, 还需依赖于数据库记录中的三个隐式字段, undo log日志, readView.  

#### 实现原理

- 记录中的隐藏字段:  
	在创建一张表时, 除了自己指定的字段, InnoDB还会自动添加三个隐式字段.  
	|   隐藏字段   | 含义 |
	|   -------   | ---- |
	| DB_TRX_ID   | 最近修改事务ID, 记录插入这条记录或最后一次修改该记录的事务ID. |
	| DB_ROLL_PTR | 回滚指针, 指向这条记录的上一个版本, 用于配合undo log, 指向上一个版本. |
	| DB_ROW_ID   | 隐藏主键, 如果表结构没有指定主键, 将会生成该隐藏字段. |

	查看指令: `ibd2sdi 表文件名`, 需要先进入其数据库中.  

- undo log日志:  
	回滚日志, 在insert, update, delete的时候产生的便于数据回滚的日志.  
	当insert的时候, 产生的undo log日志只在回滚时需要, 在事务提交后, 可被立即删除.  
	而update, delete的时候,产生的undo log日志不仅在回滚时需要, 在快照读时也需要, 不会立即被删除.  

- undo log版本链:  
	将各个版本按顺序形成链表.  
	详细演示请查看教学视频:  
	https://www.bilibili.com/video/BV1Kr4y1i7ru?p=143

- readView:  
	读视图, 是快照读SQL执行时MVCC提取数据的依据, 记录并维护系统当前活跃的事务(未提交的)id.  
	在执行select时生成readview.  
	ReadView中包含了四个核心字段:  
	| 字段           | 含义 |
	| -----------    | ---- |
	| m_ids          | 当前活跃的事务ID集合 |
	| min_trx_id     | 最小活跃事务ID |
	| max_trx_id     | 预分配事务ID, 当前最大事务ID+1(因为事务ID是自增的) |
	| creator_trx_id | ReadView创建者的事务ID |

	访问规则:  
	```
	trx_id == creator_trx_id -> 可以访问该版本  
	trx_id < min_trx_id      -> 可以访问该版本  
	trx_id > max_trx_id      -> 不可以访问该版本  
	min_trx_id <= trx_id <= max_trx_id -> 如果trx_id不在m_ids中是可以访问该版本的  
	```

	根据undo log日志链依次判断能否访问.  

## MySQL管理

### 系统数据库

MySQL(8.0)安装完成后, 自带了以下四个数据库:  
| 数据库 | 作用 |
| ----- | ---- |
| mysql | 存储MySQL服务器正常运行所需的各种信息(时区, 主从, 用户, 权限等) |
| information_schema | 提供了访问数据库元数据(数据的数据信息)的各种表和视图, 包含数据库、表、字段类型及访问权限等 |
| performance_schema | 为MySQL服务器运行时状态提供了一个底层监控功能, 主要用于收集数据库服务器性能参数 |
| sys | 包含一系列方便DBA和开发人员利用performance_schema性能数据库进行性能优化和诊断的视图 |

### 常用工具

- mysql: MySQL的客户端工具.  

	语法: `mysql [options] [database]`  
	选项:  
	```
	-u --user=name  		# 指定用户名  
	-p --password[=name]	# 指定密码  
	-h --host=name			# 指定服务器ip或域名  
	-P --port=port			# 指定连接端口  
	-e --execute=name		# 执行SQL语句并退出  
	```

	-e 可以在客户端执行SQL语句, 常用于脚本中:  
	`mysql -uroot -p1234 db_name -e "select * from table_name";`  

- mysqladmin:  
	一个执行管理操作的客户端程序. 可以用它来检查服务器的配置和当前状态, 创建并删除数据库等.  
	查看帮助文档: `mysqladmin --help`  
	帮助文档中有选项信息的介绍.  

- mysqlbinlog:  
	由于服务器生成的二进制日志文件以二进制格式保存, 所以如果想要检查这些文本的文本格式, 就会用到mysqlbinlog日志管理工具.  
	语法: `mysqlbinlog [options] log-files1 log-files2 ...`  
	选项:  
	```
	-d --database=name		# 指定数据库名称, 只列出指定的数据库相关操作.  
	-o --offset=#			# 忽略掉日志中的前n行命令.  
	-r --result-file=name	# 将输出的文本格式日志输出到指定文件.  
	-s --short-form			# 显示简单格式, 忽略掉一些信息.  
	--start-datetime=date1 --stop-datetime=date2	# 指定日期间隔内的所有日志.  
	--start-position=pos1 --stop-position=pos2		# 指定位置间隔内的所有日志.  
	```
- mysqlshow:  
	mysql客户端对象查找工具,用来很快地查找存在哪些数据库, 数据库中的表, 表中的列或者索引.  
	语法: `mysqlshow [options] [db_name[table_name[col_name]]]`
	选项:  
	```
	--count		# 显示数据库及表的统计信息(数据库, 表 均可以不指定)
	-i 			# 显示指定数据库或者指定表的状态信息
	```

	`mysqlshow -uroot -p1234 [db_name] --count/-i`

- mysqldump:  
	用来备份数据库或在不同数据库之间进行数据迁移. 备份内容包含创建表, 及插入表的SQL语句.  
	- 备份: `mysqldump -u root -p 数据库名(列表) [表名] [-t/d] > '备份保存路径与文件名(.sql)'`
		- 数据库用 -A 代替表示所有数据库, -t 表示只导出数据, -d只导出结构.

	- 还原: `mysql -u root -p 数据库名 < '备份文件路径和文件名'`
		- 如果没有数据库需要先创建, 再导入(如果只有数据的话)



# 运维

## 日志

### 错误日志

### 二进制日志

二进制日志(BINLOG)记录了所有的 DDL(数据定义语言)语句和 DML(数据操纵语言)语句,但不包括数据查询(select/show)语句。  

作用:  
1. 灾难时的数据恢复  
2. MySQL的主从复制  

MySQL8版本中,二进制日志默认为开启,查看语句:  
`show variables like '%log_bin%';`  

- 日志格式  
MySQL服务器中提供了多种格式来记录二进制日志  
|  日志格式  | 含义 |
|  -------  | ---- |
| statement | 基于sql语句的日志记录,记录的是sql语句,对数据进行修改的sql都会记录在日志文件中 |
| row(默认) | 基于行的日志记录,记录的是每一行的数据变更 |
|   mixed   | 混合了 statement 和 row 两种格式,默认采用statement,在某些特殊情况下自动切换为row进行记录 |

查看格式语句: `show variables like '%binlog_format%';`

- 日志查看
由于日志是以二进制方式存储的，不能直接读取，需要通过二进制日志查询工具 mysqlbinlog 来查看，语法(cmd)：  
`mysqlbinlog [参数选项] logfilename`  
参数选项:  
\-d 指定数据库名称,只列出指定的数据库相关操作  
\-o 忽略掉日志中的前n行命令  
\-v 将行事件(数据变更)重构为SQL语句  
\-w 将行事件(数据变更)重构为sql语句,并输出注释信息

- 日志删除  
对于比较繁忙的业务系统,每天生成的binlog数据巨大,如果长时间不清理,将会占用大量磁盘空间。

| 指令 | 含义 |
| --- | --- |
| reset master | 删除全部 binlog 日志,删除之后,日志编号将从binlog.000001开始|
| purge master logs to 'binlog.······' | 删除······编号之前的所有日志 |
| purge master logs before 'yyyy-mm-dd hh(24):mm:ss' | 删除此时间之前产生的所有日志 |

也可以在MySQL的配置文件中配置二进制日志的过期时间,自动删除过期日志(默认30天)  
`show variables like '%binlog_expre_logs_seconds%';`


### 查询日志

### 慢查询日志


## 主从复制



## 分库分表

### 介绍


### MyCat


### 分片规则


### MyCat管理与监控


## 读写分离

### 一主一从


### 双主双从

## 备份与还原

在MySQL常用工具中 mysqldump 可以用来备份以及还原.  
[常用工具](###常用工具)

### 导出  

```
select 列名(*) from table 表名 [where ...] into outfile '目标文件(.txt)' [options]  
// 目标文件不能已存在
[options]为可选参数选项
FIELDS TERMINATED BY '字符串'：设置字符串为字段之间的分隔符，可以为单个或多个字符，默认情况下为制表符‘\t’。  
FIELDS [OPTIONALLY] ENCLOSED BY '字符'：设置字符来括上 CHAR、VARCHAR 和 TEXT 等字符型字段。如果使用了 OPTIONALLY 则只能用来括上 CHAR 和 VARCHAR 等字符型字段。  
FIELDS ESCAPED BY '字符'：设置如何写入或读取特殊字符，只能为单个字符，即设置转义字符，默认值为‘\’。
LINES STARTING BY '字符串'：设置每行开头的字符，可以为单个或多个字符，默认情况下不使用任何字符。
LINES TERMINATED BY '字符串'：设置每行结尾的字符，可以为单个或多个字符，默认值为‘\n’ 。
```
导出数据有权限控制,只能导出到指定的文件夹下  
查看路径: `SHOW VARIABLES LIKE 'secure_file_priv';`  
或者更改配置信息: 在数据库的存储路径下的 my.ini 中更改`secure_file_priv=设置路径`

### 导入  

`load data local infile '文件路径' into table <表名>`  
需要权限,查看:  
`show global variables like 'local_infile';`  
更改:  
`set global local_infile = 1;`  
但仍会报错...  

解决方案:
1. cmd登录时: `mysql --locad_infile=1 -u root -p `  
2. 更改配置
3. 建议右键表格->从文件导入数据 


# 数据类型

## 整型

| 类型名称      | 取值范围                                  | 大小    |
| ------------- | ----------------------------------------- | ------- |
| TINYINT       | -128〜127                                 | 1个字节 |
| SMALLINT      | -32768〜32767                             | 2个宇节 |
| MEDIUMINT     | -8388608〜8388607                         | 3个字节 |
| INT (INTEGHR) | -2147483648〜2147483647                   | 4个字节 |
| BIGINT        | -9223372036854775808〜9223372036854775807 | 8个字节 |

无符号在数据类型后加 unsigned 关键字。

## 浮点型

| 类型名称            | 说明               | 存储需求   |
| ------------------- | ------------------ | ---------- |
| FLOAT               | 单精度浮点数       | 4 个字节   |
| DOUBLE              | 双精度浮点数       | 8 个字节   |
| DECIMAL (M, D)，DEC | 压缩的“严格”定点数 | M+2 个字节 |

## 日期和时间

| 类型名称  | 日期格式            | 日期范围                                          | 存储需求 |
| --------- | ------------------- | ------------------------------------------------- | -------- |
| YEAR      | YYYY                | 1901 ~ 2155                                       | 1 个字节 |
| TIME      | HH:MM:SS            | -838:59:59 ~ 838:59:59                            | 3 个字节 |
| DATE      | YYYY-MM-DD          | 1000-01-01 ~ 9999-12-3                            | 3 个字节 |
| DATETIME  | YYYY-MM-DD HH:MM:SS | 1000-01-01 00:00:00 ~ 9999-12-31 23:59:59         | 8 个字节 |
| TIMESTAMP | YYYY-MM-DD HH:MM:SS | 1980-01-01 00:00:01 UTC ~ 2040-01-19 03:14:07 UTC | 4 个字节 |

## 字符串

| 类型名称   | 说明                                      | 存储需求                                               |
| ---------- | ---------------------------------------- | ----------------------------------------------------- |
| CHAR(M)    | 固定长度非二进制字符串                     | M 字节，1<=M<=255                                      |
| VARCHAR(M) | 变长非二进制字符串                         | L+1字节，在此，L< = M和 1<=M<=255                      |
| TINYTEXT   | 非常小的非二进制字符串                     | L+1字节，在此，L<2^8                                    |
| TEXT       | 小的非二进制字符串                         | L+2字节，在此，L<2^16                                  |
| MEDIUMTEXT | 中等大小的非二进制字符串                   | L+3字节，在此，L<2^24                                   |
| LONGTEXT   | 大的非二进制字符串                         | L+4字节，在此，L<2^32                                  |
| ENUM       | 枚举类型，只能有一个枚举字符串值            | 1或2个字节，取决于枚举值的数目 (最大值为65535)            |
| SET        | 一个设置，字符串对象可以有零个或 多个SET成员 | 1、2、3、4或8个字节，取决于集合 成员的数量（最多64个成员） |

## 二进制类型

| 类型名称       | 说明                 | 存储需求               |
| -------------- | -------------------- | ---------------------- |
| BIT(M)         | 位字段类型           | 大约 (M+7)/8 字节      |
| BINARY(M)      | 固定长度二进制字符串 | M 字节                 |
| VARBINARY (M)  | 可变长度二进制字符串 | M+1 字节               |
| TINYBLOB (M)   | 非常小的BLOB         | L+1 字节，在此，L<2^8  |
| BLOB (M)       | 小 BLOB              | L+2 字节，在此，L<2^16 |
| MEDIUMBLOB (M) | 中等大小的BLOB       | L+3 字节，在此，L<2^24 |
| LONGBLOB (M)   | 非常大的BLOB         | L+4 字节，在此，L<2^32 |

 

# 权限一览表

> 具体权限的作用详见[官方文档](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html "官方文档")

GRANT 和 REVOKE 允许的静态权限

| Privilege                                                    | Grant Table Column           | Context                               |
| :----------------------------------------------------------- | :--------------------------- | :------------------------------------ |
| [`ALL [PRIVILEGES]`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_all) | Synonym for “all privileges” | Server administration                 |
| [`ALTER`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_alter) | `Alter_priv`                 | Tables                                |
| [`ALTER ROUTINE`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_alter-routine) | `Alter_routine_priv`         | Stored routines                       |
| [`CREATE`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_create) | `Create_priv`                | Databases, tables, or indexes         |
| [`CREATE ROLE`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_create-role) | `Create_role_priv`           | Server administration                 |
| [`CREATE ROUTINE`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_create-routine) | `Create_routine_priv`        | Stored routines                       |
| [`CREATE TABLESPACE`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_create-tablespace) | `Create_tablespace_priv`     | Server administration                 |
| [`CREATE TEMPORARY TABLES`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_create-temporary-tables) | `Create_tmp_table_priv`      | Tables                                |
| [`CREATE USER`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_create-user) | `Create_user_priv`           | Server administration                 |
| [`CREATE VIEW`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_create-view) | `Create_view_priv`           | Views                                 |
| [`DELETE`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_delete) | `Delete_priv`                | Tables                                |
| [`DROP`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_drop) | `Drop_priv`                  | Databases, tables, or views           |
| [`DROP ROLE`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_drop-role) | `Drop_role_priv`             | Server administration                 |
| [`EVENT`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_event) | `Event_priv`                 | Databases                             |
| [`EXECUTE`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_execute) | `Execute_priv`               | Stored routines                       |
| [`FILE`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_file) | `File_priv`                  | File access on server host            |
| [`GRANT OPTION`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_grant-option) | `Grant_priv`                 | Databases, tables, or stored routines |
| [`INDEX`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_index) | `Index_priv`                 | Tables                                |
| [`INSERT`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_insert) | `Insert_priv`                | Tables or columns                     |
| [`LOCK TABLES`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_lock-tables) | `Lock_tables_priv`           | Databases                             |
| [`PROCESS`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_process) | `Process_priv`               | Server administration                 |
| [`PROXY`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_proxy) | See `proxies_priv` table     | Server administration                 |
| [`REFERENCES`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_references) | `References_priv`            | Databases or tables                   |
| [`RELOAD`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_reload) | `Reload_priv`                | Server administration                 |
| [`REPLICATION CLIENT`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_replication-client) | `Repl_client_priv`           | Server administration                 |
| [`REPLICATION SLAVE`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_replication-slave) | `Repl_slave_priv`            | Server administration                 |
| [`SELECT`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_select) | `Select_priv`                | Tables or columns                     |
| [`SHOW DATABASES`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_show-databases) | `Show_db_priv`               | Server administration                 |
| [`SHOW VIEW`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_show-view) | `Show_view_priv`             | Views                                 |
| [`SHUTDOWN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_shutdown) | `Shutdown_priv`              | Server administration                 |
| [`SUPER`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_super) | `Super_priv`                 | Server administration                 |
| [`TRIGGER`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_trigger) | `Trigger_priv`               | Tables                                |
| [`UPDATE`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_update) | `Update_priv`                | Tables or columns                     |
| [`USAGE`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_usage) | Synonym for “no privileges”  | Server administration                 |

GRANT 和 REVOKE 允许的动态权限

| Privilege                                                    | Context                                           |
| :----------------------------------------------------------- | :------------------------------------------------ |
| [`APPLICATION_PASSWORD_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_application-password-admin) | Dual password administration                      |
| [`AUDIT_ABORT_EXEMPT`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_audit-abort-exempt) | Allow queries blocked by audit log filter         |
| [`AUDIT_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_audit-admin) | Audit log administration                          |
| [`AUTHENTICATION_POLICY_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_authentication-policy-admin) | Authentication administration                     |
| [`BACKUP_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_backup-admin) | Backup administration                             |
| [`BINLOG_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_binlog-admin) | Backup and Replication administration             |
| [`BINLOG_ENCRYPTION_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_binlog-encryption-admin) | Backup and Replication administration             |
| [`CLONE_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_clone-admin) | Clone administration                              |
| [`CONNECTION_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_connection-admin) | Server administration                             |
| [`ENCRYPTION_KEY_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_encryption-key-admin) | Server administration                             |
| [`FIREWALL_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_firewall-admin) | Firewall administration                           |
| [`FIREWALL_EXEMPT`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_firewall-exempt) | Firewall administration                           |
| [`FIREWALL_USER`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_firewall-user) | Firewall administration                           |
| [`FLUSH_OPTIMIZER_COSTS`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_flush-optimizer-costs) | Server administration                             |
| [`FLUSH_STATUS`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_flush-status) | Server administration                             |
| [`FLUSH_TABLES`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_flush-tables) | Server administration                             |
| [`FLUSH_USER_RESOURCES`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_flush-user-resources) | Server administration                             |
| [`GROUP_REPLICATION_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_group-replication-admin) | Replication administration                        |
| [`GROUP_REPLICATION_STREAM`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_group-replication-stream) | Replication administration                        |
| [`INNODB_REDO_LOG_ARCHIVE`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_innodb-redo-log-archive) | Redo log archiving administration                 |
| [`NDB_STORED_USER`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_ndb-stored-user) | NDB Cluster                                       |
| [`PASSWORDLESS_USER_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_passwordless-user-admin) | Authentication administration                     |
| [`PERSIST_RO_VARIABLES_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_persist-ro-variables-admin) | Server administration                             |
| [`REPLICATION_APPLIER`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_replication-applier) | `PRIVILEGE_CHECKS_USER` for a replication channel |
| [`REPLICATION_SLAVE_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_replication-slave-admin) | Replication administration                        |
| [`RESOURCE_GROUP_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_resource-group-admin) | Resource group administration                     |
| [`RESOURCE_GROUP_USER`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_resource-group-user) | Resource group administration                     |
| [`ROLE_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_role-admin) | Server administration                             |
| [`SESSION_VARIABLES_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_session-variables-admin) | Server administration                             |
| [`SET_USER_ID`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_set-user-id) | Server administration                             |
| [`SHOW_ROUTINE`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_show-routine) | Server administration                             |
| [`SYSTEM_USER`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_system-user) | Server administration                             |
| [`SYSTEM_VARIABLES_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_system-variables-admin) | Server administration                             |
| [`TABLE_ENCRYPTION_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_table-encryption-admin) | Server administration                             |
| [`VERSION_TOKEN_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_version-token-admin) | Server administration                             |
| [`XA_RECOVER_ADMIN`](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html#priv_xa-recover-admin) | Server administration                             |

# 图形化界面工具

- Workbench(免费): http://dev.mysql.com/downloads/workbench/
- navicat(收费，试用版30天): https://www.navicat.com/en/download/navicat-for-mysql
- Sequel Pro(开源免费，仅支持Mac OS): http://www.sequelpro.com/
- HeidiSQL(免费): http://www.heidisql.com/
- phpMyAdmin(免费): https://www.phpmyadmin.net/
- SQLyog: https://sqlyog.en.softonic.com/

# 小技巧

1. 在SQL语句之后加上`\G`会将结果的表格形式转换成行文本形式
2. 查看Mysql数据库占用空间：
```sql
SELECT table_schema "Database Name"
     , SUM(data_length + index_length) / (1024 * 1024) "Database Size in MB"
FROM information_schema.TABLES
GROUP BY table_schema;
```

# 关于笔记

本人下载了此篇未完成的笔记, 根据后续课程继续完善, 并结合《数据库系统概论》添加了部分理论知识.  
[https://github.com/BlankWood/study-notes/blob/main/MySQL.md](https://github.com/BlankWood/study-notes/blob/main/MySQL.md)  

**B站@守心-人 提供的后续课程笔记**  
**[https://github.com/Buildings-Lei/mysql_note/blob/main/README.md](https://github.com/Buildings-Lei/mysql_note/blob/main/README.md)**