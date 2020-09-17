





# dns服务器搭建

## 1.软件安装

bind，bind-chroot，bind-libs，*bind-utils(host,nslookup,dig命令)*

```
yum -y install bind bind-chroot bind-libs bind-utils
```

## 2.修改配置文件

 /etc/named.conf

```
10 options {
11 listen-on port 53 { any; };
12 listen-on-v6 port 53 { ::1; };
13 directory "/var/named";
14 dump-file "/var/named/data/cache_dump.db";
15 statistics-file "/var/named/data/named_stats.txt";
16 memstatistics-file "/var/named/data/named_mem_stats.txt";
17 allow-query { any; };
18 recursion yes;
19
20 // dnssec-enable yes;
21 // dnssec-validation yes;
```

第11行127.0.0.1改为192.168.11.42或any

第17行localhost改为any

第20～21行注释掉：//注释掉2行



## 3.配置解析

(1)在/etc/named.rfc1912.zones文件中定义“test.com”的正向域

```
25 zone "wgxy.com" IN { //定义“test.com”这个域
26 type master;
27 file "named.localhost"; //指向“named.localhost”或“wgxy.com.zone”文件
28 allow-update { none; };
29 };
```

(2)进入/var/named目录，复制named.localhost并改名为wgxy.com.zone

```

$TTL 1D
@       IN SOA  dns root (      ////////////////////////////删除///////////////////////////注意，这里要有两个，一个会报错    这里是dns和root
                                        0       ; serial
                                        1D      ; refresh
                                        1H      ; retry
                                        1W      ; expire
                                        3H )    ; minimum
@       NS      dns
dns     A       本地ip
ftp     A       192.168.5.66

```

最上面SOA 和NS两行必须有

这里注意，这个文件必须改为0644，不然识别不出来

vim /etc/resolv.conf   设置dns服务器

## 4.转发

options{

forwards {114.114.114.144;8.8.8.8;};

}
