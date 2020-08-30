# python 操作数据库

## 安装

```powershell
pip3 install pymysql
```

## 引用

```python
 from pymysql import *
```

### 查询流程

```python
#连接数据库
conn=connect(host='localhost',port=3306,user='root',password='123',database='bai',charset='utf8')
#设置游标
cs1=conn.cursor()

#执行命令
cs1.execute('select * from bai;')

#获取游标结果
cs1.fetchone() 
cs1.fetchall() 
cs1.fetchmany()
#关闭游标
cs1.close()
#关闭连接
conn.close()
```

### 增删改流程

```python
#其他与上面一致
#但是修改后，需要提交
conn.commit()

#错误回滚
conn.rollback()

```

防止sql注入

```python
#把查询内容放在列表里，可以防止注入
```

