#### 说明
> `cut`命令可以从一个文本文件或者文本流中提取文本列

#### 命令参数
- `-d` 后面接分割字符。与`-f`一起使用  
- `-f` 依据`-d`的分割字符将一段歇息分割成为数段，用`-f`取出第几段  
- `-c` 以字符的单位取出固定字符区间
- `-b` 仅显示行中指定范围的内容
- `-n` 与`-b`连用，不分割多字节字符

#### 实例
- *将`PATH`变量取出第五个路径*
```bash
$ echo $PATH | cut -d ':' -f 5
/root/bin
```
- *将`PATH`变量取出第三和第五个路径*
```bash
$ echo $PATH | cut -d ':' -f 3,5
/usr/sbin:/root/bin
```
- *将`PATH`变量取出第三个到最后一个路径*
```bash
$ echo $PATH | cut -d ':' -f 3-
/usr/sbin:/usr/bin:/root/bin
```
- *将`PATH`变量取出第一个到第三个路径*
```bash
$ echo $PATH | cut -d ':' -f 1-3
/usr/local/sbin:/usr/local/bin:/usr/sbin
```
- *只显示`/etc/passwd`的用户和shell*
```bash
$ cat /etc/passwd | cut -d ':' -f 1,7
root:/bin/bash
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzczOTU1MDIwXX0=
-->