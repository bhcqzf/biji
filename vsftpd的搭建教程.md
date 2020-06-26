# vsftpd的搭建教程

## 1.安装vsftpd

```
yum -y install vsftpd
```

## 2.配置vsftpd

```
(1)设置超级用户root也能正常登录FTP服务器
修改行：
# vi /etc/vsftpd/vsftpd.conf
修改行：
85 ftpd_banner=欢迎您登录到网络18级699李老师的FTP服务器！
添加行：
120
121#设置超级用户root也能正常登录FTP服务器
122userlist_deny=NO
123userlist_file=/etc/vsftpd/user_list

------------------------------------------------------------------
# vi /etc/vsftpd/user_list //红名单
已有：
7 root

# vi /etc/vsftpd/ftpusers //黑名单
注释掉第2行：
2#root

```

```
(2)设置本地用户的根目录为/var/ftp
添加行：
124 #设置本地用户的根目录为/var/ftp
125local_root=/var/ftp
```

