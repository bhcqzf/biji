# python 的open命令

## 打开文件

```python
f = open('path','w')
 	'r'       open for reading (default)
    'w'       open for writing, truncating the file first
    'x'       create a new file and open it for writing
    'a'       open for writing, appending to the end of the file if it exists
    'b'       binary mode
    't'       text mode (default)
    '+'       open a disk file for updating (reading and writing)
    'U'       universal newline mode (deprecated)
```

## 读取文件内容

```python
f = open('path','r')
f.read()
read(size=-1, /)  后面接字符大小
readline(size=-1, /)	读取文件内容，按行读，返回字符串
readlines(hint=-1, /)	读取所有，按行返回，返回列表
```

## 关闭文件

```python
f.close()
直接调用的open必须关闭
```

## 如果文件大，分片读取

```python
while 1:
	content = f.read(1024)
	if len(content) == 0:
		break
```

## 待解决：大文件排序

## 游标

```python
f.tell()   #显示游标位置
f.seek()	seek(cookie, whence=0, /) 	#第一个参数是微调，第二个参数是位置，默认0，开头
   * 0 -- start of stream (the default); offset should be zero or positive
   * 1 -- current stream position; offset may be negative
   * 2 -- end of stream; offset is usually negative
#python3中微调不能为负数
```

