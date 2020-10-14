<!-- TOC -->

- [ORACLE学习笔记](#oracle%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0)
    - [重要概念](#%E9%87%8D%E8%A6%81%E6%A6%82%E5%BF%B5)
    - [创建、删除表空间](#%E5%88%9B%E5%BB%BA%E5%88%A0%E9%99%A4%E8%A1%A8%E7%A9%BA%E9%97%B4)
    - [创建用户](#%E5%88%9B%E5%BB%BA%E7%94%A8%E6%88%B7)
    - [常见数据类型](#%E5%B8%B8%E8%A7%81%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
    - [创建表](#%E5%88%9B%E5%BB%BA%E8%A1%A8)
    - [修改表结构2](#%E4%BF%AE%E6%94%B9%E8%A1%A8%E7%BB%93%E6%9E%842)
    - [数据的增删改](#%E6%95%B0%E6%8D%AE%E7%9A%84%E5%A2%9E%E5%88%A0%E6%94%B9)
    - [序列](#%E5%BA%8F%E5%88%97)
    - [scott用户](#scott%E7%94%A8%E6%88%B7)
    - [单行函数](#%E5%8D%95%E8%A1%8C%E5%87%BD%E6%95%B0)
    - [条件表达式](#%E6%9D%A1%E4%BB%B6%E8%A1%A8%E8%BE%BE%E5%BC%8F)
    - [多行函数（聚合函数）](#%E5%A4%9A%E8%A1%8C%E5%87%BD%E6%95%B0%E8%81%9A%E5%90%88%E5%87%BD%E6%95%B0)
    - [分组查询](#%E5%88%86%E7%BB%84%E6%9F%A5%E8%AF%A2)
    - [多表查询](#%E5%A4%9A%E8%A1%A8%E6%9F%A5%E8%AF%A2)
    - [子查询](#%E5%AD%90%E6%9F%A5%E8%AF%A2)
    - [分页查询](#%E5%88%86%E9%A1%B5%E6%9F%A5%E8%AF%A2)
    - [视图](#%E8%A7%86%E5%9B%BE)
    - [索引](#%E7%B4%A2%E5%BC%95)
    - [pl/sql变量](#plsql%E5%8F%98%E9%87%8F)
    - [参考链接](#%E5%8F%82%E8%80%83%E9%93%BE%E6%8E%A5)

<!-- /TOC -->

## ORACLE学习笔记

### 重要概念
> 数据库：侧重于物理存储（硬件），一些数据文件。
> 实例：侧重于线程或者进程，一套硬件上可以运行多个实例，一般运行一个实例。
> 用户：Oracle中管理表的基本单位是用户（某用户下有几张表），MySQL中管理表的基本单位是数据库（当前数据库下有几张表）。
> 表空间：逻辑单位，当数据库很大不便于管理时，把数据库分成很多块，名为表空间 
> 数据文件：存储dbf、ora文件
    ![](../img/3-1.png)


### 创建、删除表空间
前提：超级管理员权限用户才能创建表空间，如system。
```sql
--创建名为test1的表空间，指定路径，指定大小，指定每次扩容的大小
create tablespace test_tablespace
datafile '数据库服务器目录\test_tablespace.dbf'
size 100m
autoextend on
next 10m;

--删除
drop tablespace test_tablespace;
```

### 创建用户
```sql
--在表空间test_tablespace中创建用户，名为test_user，密码为password
create user test_user
identified by password
default tablespace test_tablespace

--给用户授权，Oracle数据库有3种常用角色
--connect（连接角色，基本角色）、resource（开发者角色）、dba（超级管理员角色）
--给用户test_user授予dba角色
grant dba to test_user;
```

### 常见数据类型
| 数据类型             | 描述                                             |
|------------------|------------------------------------------------|
| Varchar、Varchar2 | 常用Varchar2，可自动将长度减小为适合存入的数据，都不能扩展              |
| NUMBER           | NUMBER(2)表示长度为n的整数，NUMBER(m,n)表示长度为m的小数，小数部分n位 |
| DATE             | 日期类型                                           |

### 创建表
```sql
--先名词，后类型
create table person(
    pid number(20),
    pname varchar21(10)
);
```

### 修改表结构2
```sql
--添加列,pid和pname--
alter table person add (pid number(1),pname varchar2(10)); 
--修改列类型，pid列由number(1)变为char(1)--
alter table person modify pid char(1);
--修改列名称,pid变为sex--
alter table person rename column pid to sex;
--删除列,sex--
alter table person drop column sex;
```

### 数据的增删改
```sql
--添加一条记录--
insert into person (pid,pname) values(1,'小明');
commit;
--修改一条记录--
update person set name = '小飞' where pid = '1'
commit;
--三个删除--
---删除表中全部记录
delete from person;
---删除表结构
drop table person;
---先删除表，再次创建表，效果等同于删除表中全部记录
---在数据量大的情况下，尤其是表中带有索引的情况下，会先删除索引，所以该操作效率高
---索引可以提高查询效率，但是会影响增删改效率
truncate table person;
```

### 序列
> 默认从1开始，依次递增，主要用来给主键赋值使用
> 序列不真的属于任何一张表，但是可以逻辑和表做绑定
```sql
create sequence s_person;
--dual是虚表，只是为了补全语法，无任何意义
--nextval一直递增，currval一直是当前值
select s_person.nextval from dual;

--添加一条记录，用s_person.nextval--
insert into person (pid,pname) values(s_person.nextval,'小明');
commit;
```

### scott用户
> 密码默认是tiger
> 后面的演示都使用scott用户下的表
```sql
--超级管理员权限解锁scott用户
alter user scott account unlock;
--解锁scott用户的密码，此句也可以重置密码
alter user scott identified tiger;
```

### 单行函数
> 单行函数：作用于一行，返回一个值
> 多行函数：作用于多行，返回一个值
```sql
--字符函数upper()和lower()--
select upper('yes') from dual;
--数值函数，四舍五入，保留1位，即26.2，保留-1位，即30
select round(26.18,1) from dual;
--截取函数，保留1位即56.1
select trunc(56.16,1) from dual;
--求余函数，1
select mod(10,3) from dual;
--日期函数
---查询emp表中所有员工入职距离现在几天
select sysdate-e.hiredate from emp e;
---明天此刻
select sysdate+1 from dual;

--日期转换字符串函数, 0
select to_char(sysdate,'yyyy-mm-ss hh:mi:ss') from dual;
select to_char(sysdate,'yyyy-mm-ss hh24:mi:ss') from dual;
--字符串转日期函数
select to_date('2020-10-10 21:07:52','yyyy-mm-ss hh:mi:ss') from dual;

--通用函数nvl()，如果e.comm不是null，则使用，否则为0
---null和任意值做算术运算，结果都是null
select e.sal*12+nvl(e.comm, 0) from emp e;
```

### 条件表达式
```sql
--给emp表种员工起中文名
select e.name,
    case e.name
        when 'hiccup' then '曹操'
            when 'tom' then '大猫'
                when 'sms' then '史密斯'
                    else '无名'
                        end
from emp e;

--判断emp表中员工工资，如果高于3000显示高收入，如果在1500和3000之间，显示中等收入，其余显示低收入
select e.sal,
    case e.name
        when e.sal>3000 then '高收入'
            when e.sal>1500 then '中等收入' 
                                else '低收入'
                    end
from emp e;
```
--注意：Oracle一般都用单引号

### 多行函数（聚合函数）
```sql
--注意，一次执行多行要有分号
select count(1) from emp;
select sum(sal) from emp;
select max(sal) from emp;
select avg(sal) from emp;
```

### 分组查询
```sql
--查询出每个部门的平均工资
---分组查询中，出现在gruop by后天的原始列，才能出现在select后面
---没有出现在group by后面的原始列，想在后面出现，必须加上聚合函数
select e.deptno,avg(e.sal)
from emp e
group by e.deptno
```

```sql
--查询公司高于2000的部门信息
---所有条件都不能使用别名判断，因为条件的优先级大于select
select e.deptno,avg(e.sal)
from emp e
group by e.deptno
having avg(e.sal)>2000
```

```sql
--查询出每个部门工资高于800的员工的平均工资

select e.deptno,avg(e.sal)
from emp e
where e.sal>800
group by e.deptno
```

```sql
---where过滤分组前的数据，having过滤分组后的数据
---位置表现为在group by前后
select e.deptno,avg(e.sal)
from emp e
where e.sal>800
group by e.deptno
having avg(e.sal)>2000
```

### 多表查询
```sql
--笛卡尔积，14*4=56条
select * 
from emp e, dept d;

--等值连接，14条
select * from emp e,dept d
where e.deptno = f.deptno;
```

### 子查询
```sql
--返回一个值
select * from emp where sal in
(select sal from emp where name = 'xiaoming');

--返回一个集合
select * from emp where sal in
(select sql from emp where deptno = '10');

--返回一张表，多行记录
select t.deptno, t.s, e.name, d.dname
from (
    select deptno,min(sal) s
    from emp
    group by deptno
) t,emp e,dept d
where t.deptno = e.deptno
and t.s = e.sal
and e.deptno = d.deptno;
```

### 分页查询
```sql
--只有做select查询的时候，才会有rownum

select * from (
    select rownum rn, tt.* from(
            select * from emp order by sql desc--无论这行多少条，根据11和5的值都可以分页显示
    ) tt where rownum<11
)
where rn>5
```

### 视图
```sql
--视图：提供一个查询的窗口，所有数据来自于原表，所以修改视图的数据，也就是修改对应原表里的数据
---创建视图必须要有dba权限，查询语句可以跨用户查询
---利用查询语句创建表
create table emp as select * from scott.emp;
---创建视图 
create view v_emp as select ename,job from emp;
---查询视图
select * from v_emp;
---修改视图，所有数据来自于原表，所以修改视图的数据，也就是修改对应原表里的数据
update v_emp set job = 'clerk' where where ename = 'aline';
commit;
---创建只读视图
create view v_emp as select ename,job from emp with read only;
---视图的作用：屏蔽敏感字段，保证总部和分部数据及时统一（分部使用总部做的视图）
```

### 索引
```sql
--索引：在表的列上构建一个二叉树（例如书的目录），可以提高查询效率，降低增删改效率。
---单列索引，触发规则：条件必须是索引列的原始值，单行函数，模糊查询都会影响索引的触发。
create index idx_ename on emp ename;
select * from emp where ename = 'scott';--触发单列索引
---复合索引，触发规则：第一列为优先检索列，若要触发索引，必须包含有优先检索列中的原始值
create index idx_ename_job on emp (ename,job);
select * from emp where ename = 'scott' and job  = 'tt';--触发复合索引
select * from emp where ename = 'scott' or job  = 'tt';--不触发索引
select * from emp where ename = 'scott';--触发单列索引
```

### pl/sql变量
```sql
--pl/sql编程语言是对sql语言的扩展，使得sql语言有过程化编程特性，主要用来编写存储过程和存储函数。
---申明方法，可以使用":="赋值，也可以使用into查询语句赋值，
declare
    i number(2) := 10;
    s varchar2(10) := '小明';
    ena emp.ename%type;---引用型变量
    emprow emp%rowtype;---记录型变量
begin
    dbms_output.put_line(i);
    select ename into ena from emp where empno = '7878'; 
    select * into emprow from emp where empno = '7878'; 
    dbms_output.put_line(emprow.ename || '的工作为：' || emprow.job);
end;
```

### 参考链接
[视频教程](https://www.bilibili.com/video/BV1aE411K7u8)