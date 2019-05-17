#### 说明
>  uniq命令可以去除排序过的文件中的重复行,因此uniq经常和sort合用。也就是说,为了使uniq起作用,所有的重复行必须是相邻的。

#### 语法
```bash
$ uniq [-icu]
```

#### 参数
- `-i` 忽略大小写字符的不同
- `-c` 进行计数
- `-u` 只显示唯一的行

#### 示例
```bash
# test
$ cat test
hello
world
friend
hello
world
hello
```

- 排序文件,默认是去重
```bash
$ cat test | sort | uniq
hello
world
```
- 排序文件,同时在行首位置输出该行重复的次数
```bash
$ cat test | sort | uniq -c
      4 hello
      3 world
```
- 仅显示不重复的行
```bash
$ cat test | sort | uniq -u
friend
```