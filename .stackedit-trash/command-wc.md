#### 说明
> 统计文件里面有多少单词,多少行,多少字符

#### 语法
```bash
$ wc [-lwm]
```

#### 参数
- `-i` 仅列出行
- `-w` 仅列出多少字
- `-m` 多少字符

#### 示例
- 默认使用`wx`统计`/etc/passwd`
```bash
$ wc /etc/passwd
# 20是行数 28是单词数 879是字符数
 20  28 879 /etc/passwd
```
- 统计`/etc/password`行数
```bash
$ wc -l /etc/passwd
20 /etc/passwd
```
- 统计`/etc/password`单词数
- 统计`/etc/password`字符数
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjEyNTI2MTE0NV19
-->