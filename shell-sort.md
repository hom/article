#### 说明
> 对指定文件中的行排序，并将结果写到标准输出。如果File指定多个文件，那么`sort`会将这些文件连接起来当做一个文件处理

#### 语法
```bash
$ sort [-fbMnrtuk] [File or Stdin]
```

#### 参数
- `-f` 忽略大小写差异  
- `-b` 忽略最前面的空格符部分  
- `-M` 以月份的名字来排序  
- `-n` 使用`纯数字`进行排序（默认以文字排序）  
- `-r` 反向排序  
- `-u` 就是`uniq`，相同的数据，仅出现一行列表  
- `-t` 分隔符，默认以`Tab`键来分隔  
- `-k` 以哪个区间[`field`]来进行排序

#### 示例
- 对`/etc/password`进行排序
```bash
$ cat /etc/passwd | sort
# sort 默认是以顶一个数据来排序，默认以字符串形式来排序，默认为升序
adm:x:3:4:adm:/var/adm:/sbin/nologin
bin:x:1:1:bin:/bin:/sbin/nologin
...
```
- 对`/etc/password`以第三栏进行排序
```bash
$ cat /etc/passwd | sort -t ':' -k 3
root:x:0:0:root:/root:/bin/bash
operator:x:11:0:operator:/root:/sbin/nologin
...
```
- 对`/etc/password`以第三栏进行排序，按照数字来排序
```bash
$ cat /etc/passwd | sort -t ':' -k 3 -n
# 或者
# cat /etc/passwd | sort -t ':' -k 3n
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
...
```
- 对`/etc/password`以第三栏进行排序，按照数字来排序，使用倒序排列
```bash
$ cat /etc/passwd | sort -t ':' -k 3 -n -r
# cat /etc/passwd | sort -t ':' -k 3 -nr
#cat /etc/passwd | sort -t ':' -k 3nr
polkitd:x:999:998:User for polkitd:/:/sbin/nologin
chrony:x:998:996::/var/lib/chrony:/sbin/nologin
...
```
- 对`/etc/password`先以第六个域的第2个字符到第4个字符进行正向排序,再基于第一个域进行反向排序
```bash
$ cat /etc/passwd | sort -t ':' -k 6.2,6.4 -k 1r
bin:x:1:1:bin:/bin:/sbin/nologin
root:x:0:0:root:/root:/bin/bash
operator:x:11:0:operator:/root:/sbin/nologin
...
```
- 对`/etc/password`有多少个shell:对/etc/passwd的第七个域进行排序,然后去重
```bash
$ cat /etc/passwd | sort -t ':' -k 7 -u
bin:x:1:1:bin:/bin:/sbin/nologin
root:x:0:0:root:/root:/bin/bash
...
```