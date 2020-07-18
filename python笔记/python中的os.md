# python中的os

## 重命名

```python
rename(src, dst, *, src_dir_fd=None, dst_dir_fd=None)
#只能在同一文件夹下重命名，否则报错“[WinError 17] 系统无法将文件移到不同的磁盘驱动器”
#不同文件夹  使用import shutil
# 移动文件（目录）和rename用法一样。
shutil.move("oldpos","newpos") 
```

## 创建文件（夹）

```python
#文件
os.open('path','w')
mkdir(path, mode=511, *, dir_fd=None)


```

## 获取目录

```
os.getcwd()

```

## 更改目录

```
os.chdir()
```

## 获取目录列表

```
os.listdir()

```

## 删除目录

```
os.rmdir()
os.removedirs()  #递归删除   如果文件夹不为空  报错
```

