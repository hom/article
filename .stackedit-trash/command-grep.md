## grep命令

### 命令简介
`grep`是`Linux`中强大的文本搜索工具，命令格式为`grep [option] <pattern> file`
### 命令参数
- `-a` `--text` #不要忽略二进制的数据
- `-A`<显示行数> `--after-content`=<显示行数> #除了显示符合匹配样式的那行之外，并显示该行之后的内容
- `-b` `--byte-offset` #在显示符合样式的那一行之前，标识出该行第一个字符的编号
- `-B`<显示行数> `--before-content`=<显示行数> #除了显示匹配的那行之外，显示该行之前的内容
- `-c` `--count` #计算匹配的行数
- `-C`<显示行数> `--content`=<显示行数>或-<显示行数> #除了显示匹配行的内容，显示匹配行之前后的内容
- `-d`<动作> `--directories`=<动作> #当指定查找的是目录而不是文件时，必须使用该参数，否则grep会回报信息并停止动作
- `-e`<范本样式> `--regexp`=<范本样式> #将指定字符串作为查找文件内容的样式
- `-E` `--extented-regexp` #将样式为延伸的普通表示法使用
- `-f`<规则文件> `--file`=<规则文件> #指定规则文件，其内容有一个或多个规则样式，让grep查找符合规则的文件内容，格式为每行一个规则文件
- `-F` `--fixed-regexp` #将样式视为固定字符串的列表
- `-G` `--basic-regexp` #将样式视为普通的表示法使用
- `-h` `--no-filename` #在显示符合样式的那一行之前，不标识该行所属的文件名称
- `-H` `--with-filename` #在显示符合样式的哪一行之前，标识该行所属的文件名称
- `-i` `--ignore-case` #忽略字符大小写的区别
- `-l` `--file-with`-matches #列出文件内容符合指定的样式的文件名称
- `-L` `--file-without`-matches #列出文件内容不符合指定样式的文件名称
- `-n` `--line-number` #在现实符合样式的那一行之前，标识出该行的列数编号
- `-q` `--quit`或`--silent` #不显示任何信息
- `-r` `--recursive` #和制定`-d recursive`参数相同，标识递归
- `-s` `--no-message` #不显示错误信息
- `-v` `--revert-match` #显示不包括匹配文本的所有内容
- `-V` `--version` #显示版本信息
- `-w` `--word-regexp` #只显示全字符合的列
- `-x` `--line-regexp` #只显示全列符合的列
- `-y` #此参数的效果和指定`-i`参数相同
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2OTI5MTYxNl19
-->