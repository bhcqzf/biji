# DQL 查询语句 mysql

## 1.简单查询

### 查询所有字段

```mysql
select * from 表名;
```

### 查询指定字段

```mysql
select name,id from 表名;
```

### 别名

```mysql
select name as 姓名 from 表名;
select name    姓名 from 表名;
```

### 表名.字段

```mysql
select 表名.name,表名.id from 表名;
```

### 给表取别名

```mysql
select f.name,f.id from 表名 as f;
```

### 去除重复

```mysql
select  distinct name from 表名;
```

## 2.条件查询

### 比较运算符

\>    \<

```mymysql
select * from 表名 where id > 10;
select * from 表名 where id < 10;
select * from 表名 where id = 10;
select * from 表名 where id <= 10;
select * from 表名 where id >= 10;
```

\<>=

```mysql
select * from 表名 where id <> 10;
select * from 表名 where id != 10;
```

### 逻辑运算符

#### and

```mysql
select * from bai where id >17 and id <28;
 select * from bai where id >17 and name ='bai';
```

#### OR

```mysql
select * from bai where id >17 or name ='bai';
```

#### NOT

```mysql
select * from bai where not id <17 or name ='bai';   --否定一个条件
select * from bai where not (id <17 or name ='bai'); --否定全部条件
```

## 3.模糊查询

### like

```mysql
--%代表多个字符  _ 代表一个字符

select * from bai where name  like '%ba%';
select * from bai where name  like '%ba_';
```



### rlike

```mysql
--正则匹配
select * from bai where name  rlike '^ba*';
```

## 2.范围查询

#### 范围

```mysql
--在一定范围内
select * from bai where id in (1,5,15);

--不在一定范围内
select * from bai where id  not in (1,5,15);

--连续的范围
select * from bai where id  BETWEEN 10 and 18;

--不在范围内
select * from bai where id  not  BETWEEN 10 and 18;
--select * from bai where id  not  (BETWEEN 10 and 18); --这种用法是错的
```

#### null

```mysql
select * from bai where name is null;
select * from bai where name is  not null;
```

## 4.排序

```mysql
--正向排序  asc可省略
select * from bai where (id between 18 and 21) and sex='m' order by id asc ;

--反向排序
select * from bai where (id between 18 and 21) and sex='m' order by id desc ;

--多字段排序
select * from  bai order by name desc,id desc;
```

## 5.聚合函数

```mysql
--总数 count
select count(*) from  bai where name = 'bai' ;

--最大值 max
select max(id) from bai;

--最小值 min
select min(id) from bai;

--求和 sum
select sum(id) from bai;

--平均值 avg
select avg(id) from bai;
select sum(id)/count(*) from bai;  --先求和再平均

--四舍五入 保留小数 round(数,2)  数，小数位数
 select round(sum(id)/count(*),1) from bai;  --保留了一位小数
 
 

```

## 6.分组（一般和聚合一起用）

```mysql
--group by 分组   一般和聚合一起用  不然没什么用
select sex,count(*) from bai group by sex;

--显示组里有什么人
 select sex,group_concat(name) from bai group by sex;
 
 select sex,group_concat(name,id) from bai group by sex;
 select sex,group_concat(name,"_",id) from bai group by sex;--中间可以用下划线分割
 
--组聚合数量大于2
select sex,group_concat(name,'_',id) from bai group by sex having count(*) >2;


```

```sql
--having 和where的区别
--原表中有的字段  使用where
--原表中没有的使用having
```

## 7.分页

```mysql
--只显示2个
select sex from bai limit 2;

--显示开始  count
select sex from bai limit 0,5;  --从0开始  往下数5个

--一般分页
--limit （第n页-1）*每页个数，每页个数
```

## 8.连接查询（多表查询）

#### 内连接  inner join

```mysql
--把两个表很简单的 排列组合 合起来  但一般有问题   inner join    --相当交集
select * from bai INNER JOIN ming;   --会出问题

--连接查下 on后面加条件  
select * from bai inner join ming on bai.id=ming.id;

--显示具体的值
select bai.name,ming.name,ming.id from bai inner join ming on bai.id=ming.id;
select b.name,m.name,m.id from bai as b  inner join ming as m on b.id=m.id;
```

####  左连接  left join

```mysql
--以左边表为准  没有的用null补充
select * from bai left join ming on  bai.id= ming.id;
```





#### 右链接  right join

```mysql
--以右边表为准  没有的用null补充
select * from bai right join ming on  bai.id= ming.id;
```

## 9.自关联



```mysql
--这里注意  自关联自己的时候一定要取一个别名 不然报错
select * from china inner join  china as c  on  china.id = c.pid where china.name='河北省';
select * from china inner join  china as c  on  china.id = c.pid where china.name='青岛市';
```

## 10.子查询

```mysql
--子查询
--比自关联慢
select * from china where id = (select max(id) from china);
```

