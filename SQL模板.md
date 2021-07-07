# SQL模板

## 查询操作

### WHERE 条件表达式

| 条件     | 符号                                   |
| -------- | -------------------------------------- |
| 比较大小 | =,>,<,>=,<=,!=,<>,!<,!>,NOT 加描述符号 |
| 确定范围 | between and,not between and            |
| 确定集合 | in,not in                              |
| 字符匹配 | like(%,\_),not like(%,\_)              |
| 空值     | is null,is not null                    |
| 多重条件 | and,or,not                             |

between and 案例：查询年龄为18或19岁学生的姓名

``` sql
select sname
from student
where sage between 18 and 19;
```



### 聚集函数

| 作用               | 语法                          |
| ------------------ | ----------------------------- |
| 统计元组个数       | COUNT([DISTINCT\|ALL] *)      |
| 统计一列值的个数   | COUNT([DISTINCT\|ALL] <列名>) |
| 统计一列值的总和   | SUM([DISTINCT\|ALL] <列名>)   |
| 统计一列值的平均值 | AVG([DISTINCT\|ALL] <列名>)   |
| 统计一列值的最大值 | MAX([DISTINCT\|ALL] <列名>)   |
| 统计一列值的最小值 | MIN([DISTINCT\|ALL] <列名>)   |

### 分组

可以使用 GROUP BY 查询结果做分组。

例如：查询男生和女生的人数。

```sql
select ssex,count(sno)
from student
group by ssex;
```

对分组设置限制条件使用 HAVING 关键字

例如：查询至少有两个学生选修的课程

``` sql
select cno,count(cno)
from sc
group by cno,having count(sno)>=2;
```

### 多表查询

#### 等值连接

例如：查询刘佳同学选修的所有课的课程号

``` sql
select cno
from student,sc
where sc.sno=student.sno
and sname='刘佳';
```

#### 内连接

例如：查询刘佳同学选修的所有课的课程号

``` sql
select cno
from student inner join sc
on student.sno=sc.sno
where sname='刘佳';
```

### 嵌套查询

例如：查询刘佳同学选修的所有课的课程号

``` sql
select cno
from sc
where sno in
	(
    	select sno
        from student
        where sname='刘佳';
    );
```

子查询还可以出现在select中

例如：查询每个学生的基本信息以及平时成绩

``` sql
select student.*,
(
	select avg(grade)
    from sc
    where sno=student.sno
    group by sno
)as avg_grade
from student;
```

## 插入操作

### 插入单行

例如：向学生表 student 插入一个新学生信息

``` sql
insert into student
values('160610106','周圆圆','女',20,'computer');
```

### 插入多行

插入多行操作一般是插入子查询的结果

例如：

创建一个新表 student3 ，用来存放所有学生的姓名和所在系

``` sql
create table student3
(
	sname char(20),
    sdept char(50)
)
```

向表 student3 插入数据

``` sql
insert
into student3(sname,sdept)
select sname.sdept
from student;
```

## 修改操作

### 修改数据

例如：将 database 系所有的学生年龄增加1

``` sql
update student
set sage=sage+1
where sno='database';
```

## 删除操作

### 删除数据

例如：删除 刘佳 学生信息

``` sql
delete
from student
where sname='刘佳';
```

例如：删除全体学生信息

``` sql
delete
from student;
```

## 视图

**视图**是从一个或几个表导出的表，它是虚拟的表，DBMS只保存它的定义，对视图的所有操作都将转化为对基表的操作，基表的数据变化会影响视图的数据。

### 创建视图

语法：

``` sql
create view <视图名称>[(<列名1>[,<列名2>···)]
as <子查询>
[with check option];
```

例如：建立computer系学生选课情况视图

``` sql
create view v_com_grade(sno,sname,sage,grade)
as
select student.sno,sname,sage,grade
from student,sc
where student.sno=sc.sno and sdept='computer';
```

### 修改视图

修改视图实际上就是修改视图定义，用新的子查询代替原来视图定义中的子查询。

语法：

``` sql
alter view <视图名>
as <子查询语句>;
```

例如：把定义为 computer 系学生视图修改为 network 系的学生视图

``` sql
alter v_com_student
as
select *
from student
where sdept='network';
```

### 删除视图

语法：

``` sql
drop view <视图名>
```

### 查询视图

用户可以像查询基表一样的查询视图，语法一致，对视图的查询都转化为对基表的查询

例如：视图 v_com_student 定义的是计算机系的学生信息

``` sql
select *
from v_com_student
where ssex='女';
```

这个查询可以转化为

``` sql
select *
from student
where sdept='computer' and ssex='女';
```

### 更新视图

由于视图的数据来自基表，所以对视图的更新（插入、删除、修改）都将转化为对基表的更新

1. #### 插入：

   例如：

   ``` sql
   insert
   into v_com_student
   values('160620107','何敏','男',20,'computer');
   ```

   它将转化为：

   ``` sql
   insert
   into student
   values('160620107','何敏','男',20,'computer');
   ```

2. #### 修改

   例如：

   ``` sql
   update v_com_student
   set sname='张雷'
   where sno='160610103';
   ```

   它将转化为：

   ``` sql
   update student
   set sname='张雷'
   where sno='160610103';
   ```

3. #### 删除

   例如：

   ``` sql
   delete
   from v_com_student
   where sno='160610103';
   ```

   它将转化为：

   ``` sql
   delete
   from student
   where sno='160610103';
   ```
## 数据库编程

基本语法

``` sql
declare //定义部分
	//定义变量、常量、游标、异常等
begin
	//执行部分，sql语句、流程控制语句
end;
```

### 变量

- #### 定义变量和赋值

  局部变量以 @ 开头，全局变量以 @@ 开头

  语法为：

  ``` sql
  declare @variable datatype;
  ```

  例如：

  ``` sql
  use student;
  go
  declare @rowsreturn int;
  set @rowsreturn=(select count(*) from student);
  select @rowsreturn;
  ```

  上面使用 set 赋值，也可以使用 select 直接赋值

  ``` sql
  use student;
  go
  declare @rowsreturn int;
  select @rowsreturn=count(*) from student);
  select @rowsreturn;
  ```


### IF 语句

语法

``` sql
if <布尔逻辑表达式>
	{sql语句块}
else
	{sql语句块}
```

一般 if 会配合 begin-end 使用

例如：

``` sql
if (select avg(grade) from sc where sno='201015121' group by sno) >= 60
begin
	print 'pass'
end
else
begin
	print 'not pass'
end
```

### 多分支语句

例如：

``` sql
select sno as 学号,
	课程名称=case cno
		when 1 then '数据库'
		when 2 then '数学'
		when 3 then '信息系统'
		end,
	考试等级=case
		when grade>=90 then '优秀'
		when grade>=80 then '良好'
		when grade>=70 then '中'
		when grade>=60 then '及格'
		else '不及格'
		end
from sc;
```

### 循环语句

语法：

``` sql
while <布尔逻辑表达式>
{sql语句块}
```

例如：创建一个test表，并向其中插入1000行数据

``` sql
create table test(id int identity(1,1),sname char(10));
	go
	declare @i int;
	set @i=1;
	where @i<1000
	begin
	insert into test(sname) values('tom');
	set @i=@i+1;
	end
```

### 存储过程与函数

**存储过程**是一组编译好的存储在数据服务器上，完成某一特定功能的程序代码块，他可以有输入和输出值

**函数**是另一类命名程序块，它完成某一特定功能可以持久保存

1. #### 存储过程

   **存储过程**是一组编译好的存储在数据库服务器上完成某一特定功能的程序代码块，它可以有输入参数和返回值。存储过程分为系统提供的存储过程和用户自定义的存储过程

   优点：

   1. 由于执行存储过程时保存的是已经编译好的代码块，所以可以直接调用执行，这样效率高
   2. 像函数一样模块化编程可以反复调用执行
   3. 使用存储过程降低客户机和服务器的通信量，客户端只通过网络向服务器发送调用存储过程的名称和参数，就可以调用执行，而不用发送程序本身，这样大大减少了程序量
   4. 由于从客户端传输到服务端的仅仅是存储过程的名字和参数，保存在服务器的已经是编译过的存储过程，并且具有相应权限的用户才可以执行，因此安全性更高

   语法：

   ``` sql
   create proc | procedure <存储过程名称>
   [
       {@参数 数据类型} [=默认值] [output],
       {@参数 数据类型} [=默认值] [output],
       ···
   ]
   as
   <存储过程体>
   ```

   执行：

   ``` sql
   exec [ute] {[@整形变量=]<存储过程名>}[[@参数名=]
   [{值|@变量 [output] | [default]}[,···n]]
   ```

   说明：@整形变量用于保存存储过程中 return 返回的值

   删除：

   ``` sql
   drop <proc | procedure> <存储过程名称>
   ```

2. #### 函数

   函数是另一类命名块，它完成某一特定功能并可以持久保存。函数分系统函数和用户自定义函数，函数的定义和存储过程类似，但函数调用必须指定返回类型

   语法：

   ```sql
   create function <函数名称>([@用户自定义形式参数] [as] [参数的数据类型] [=default] [,···n])
   returns <返回的数据类型>
   as
   begin
   <函数体>
   return <返回表达式>
   end
   ```

   删除：

   ``` sql
   drop function <函数名称>
   ```

### 触发器

**触发器**实际上是一类特殊的存储过程，但它不是由用户调用触发，而是当满足条件时由系统自动触发执行

作用：

1. 触发器可以实现比约束更为复杂的数据约束规则，在数据库中的数据完整性约束行为一般用check约束来实现，但是check约束一般只能引用本表的列，不能引用其他表中的属性列或者其他数据库对象，而触发器可以；除此之外，触发器还能完成比较复杂的逻辑。
2. 触发器可以实现对相关表的级联修改
3. 可以修改其他表里的数据
4. 对于视图的插入、删除、修改操作，可以转化为对基本表的操作
5. 可以在触发器中调用一个或多个存储过程
6. 可以更改原本要操作的SQL语句

语法：

``` sql
create trigger <触发器名称>
on <表名|视图名>
{for | after | instead of}
{[insert] [,] [upadte] [,] [delete] [,]}
as
<语句块>
```

删除操作：

``` sql
drop trigger <触发器名称>
```

### 游标

sql 语句的执行结果只能是整体处理，不能一次处理一行，而当查询返回多行记录时，只能通过游标对结果集中的每行进行处理。**游标**类似程序设计语言中的指针

步骤：

1. 定义游标，游标在使用之前必须先定义
2. 打开游标，游标定义之后，在使用它之前需要先打开，使其指向第一条 sql 记录
3. 推进游标，移动游标指针，可以遍历游标里的所有记录，进行逐行处理
4. 关闭游标，释放游标占用的资源

语法：

``` sql
declare <游标名称> cursor [local | global]
[forward_only | scroll]
[static | keyset | dynamic | fast_forward]
[read_only | scroll_lock | optimistic]
[type_warning]
for [建立游标的sql语句]
[for update [of column_name [,···n]]]
[:]
```

## 数据库安全

### 存取控制概述

定义用户权限，并将用户权限登记到数据字典中。用户或应用程序使用数据库的方式称为权限。在数据库系统中对用户或应用程序权限定义称之为授权。这些授权定义经过编译后存放在数据字典中，被称之为“安全规则”或“授权规则”

存取控制的级别：

- 自主存取控制

  在自主存取控制机制中，用户对不同数据库对象有不同的存取权限，不同的用户对同一对象也有不同的权限，用户可以将其拥有的存取权限转授给其他用户，因此自主存取控制非常的灵活

- 强制存取控制

  在强制存取控制机制中，每个数据库对象被标以一定的密级，每个用户也被授予某一个级别的许可证。对于任意一个对象，只有具有合法的许可证的用户才可以存取。相当于DAC，强制存取控制更严格一些

- 多级存取控制

  较高的安全级别提供的安全保护要包含较低级别的所有保护，因此，在实现强制存取控制时首先要实现自主存取控制。自主存取控制与强制存取控制共同构成数据库管理系统SQL层的安全机制。系统首先进行自主存取控制检查，对通过自主存取控制的运行存取数据对象再进行强制存取控制检查，只有通过强制存取控制检查的数据对象方可被用户存取

### 自主存取控制

#### 授权

授权有两层意思：授予予收回

- 权限授予

  grant 语句

  语法：

  ``` sql
  grant <权限> [,<权限>]...
  on <对象类型> [,<对象名>]
  to <用户> [,<用户>]...
  [with grant option];
  ```

  说明：

  如果指定了 with grant option 子语句，则获取该权限的用户可以把这种权限再授予其他用户，但被授权者不能把这种权限回授给授权者或授权者祖先

- 权限收回

  revoke 语句

  语法：

  ```sql
  revoke <权限> [,<权限>]···
  on <对象类型> [,<对象名>]
  from <用户> [,<用户>]···[cascade | restrict];
  ```

#### 角色

**角色**是被命名的一组数据库权限的集合。为了方便权限管理，可以为具有相同权限的用户创建一个管理单位。角色被授予给一个用户，用户就继承角色上的所有权限

1. 创建角色

   ``` sql
   create role <角色名>
   ```

2. 给角色授权

   ``` sql
   grant <权限> [.<权限>]···
   on <对象类型> [,<对象名>]
   to <角色> [,<角色>]···
   ```

3. 将角色授予其他用户或角色

   ``` sql
   grant <角色1> [,<角色2>]···
   to <用户> [,<角色3>]···
   [with admin option];
   ```

























