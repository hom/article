# Linux命令行与Shell脚本

## 基本脚本
### 把命令输出赋给变量
- 使用反引号`` ` ``字符
- 使用`$()`格式
### 只有数学运算
- `expr`命令
- 使用方括号`$[]`
- 浮点数使用`bc`命令
- 在脚本中使用`bc`命令处理浮点数`$(echo "option; expression" | bc))`

## 结构化命令
### `if-then`
#### `if-then`命令
```bash
if command
then
  commands
fi
# or
if command; then
  commands
fi
```
#### `if-then-else`
```bash
if command
then
  commands
else
  commands
fi
```
#### `if-then-elif`
```bash
if command1
then
  commands
elif command2
then
  more commands
fi
```
### `test`命令
```bash
if test condition
then
  commands
fi
# 使用[]
# 支持数值比较
# 字符串比较
# 文件比较  
if [ condition ]
then
  commands
fi
```
#### 数值比较

 比较|描述
----------|-----------
`n1 -eq n2` | 相等
`n1 -ge n2` | 大于或等于
`n1 -gt n2` | 大于
`n1 -le n2` | 小于或等于
`n1 -lt n2` | 小于
`n1 -ne n2` | 不等于
#### 字符车比较

比较|描述
-------------|-----------
`str1 = str2`  | 是否相同
`str1 != str2` | 是否不同
`str1 < str2`  | 小于
`str1 > str2`  | 大于
`-n str1`      | 长度是否非零
`-z str1`      | 长度是否为零
#### 文件比较

比较|描述
-------------|-------------
`-d file` | 是否是一个目录
`-e file` | 是否存在
`-f file` | 是否存在并是一个文件
`-r file` | 是否存在并可读
`-s file` | 是否存在并非空
`-w file` | 是否存在并可写
`-x file` | 是否存在并可执行
`-O file` | 是否存在并属于当前用户
`-G file` | 是否存在并且默认组与当前用户相同
`file1 -nt file2` | file1是否比file2新
`file1 -ot file2` | file1是否比file2旧

#### 符合条件测试

`if-then`语句与使用布尔逻辑组合测试

- [ condition1 ] && [ condition2 ]
- [ condition1 ] || [ condition2 ]

### `if-then`高级特性

#### 用于数学表达式的双括号  
**命令格式**  

` (( expression )) `  

**命令**  

符号 | 描述
----|----
`val++` | 后增
`val--` | 后减
`++val` | 先增
`--val` | 先减
`!` | 逻辑求反
`~` | 位求反
`**` | 幂运算
`<<` | 左位移
`>>` | 右位移
`&` | 位布尔和
`|` | 位布尔或
`&&` | 逻辑和
`||` | 逻辑或

#### 用于高级字符串处理功能的双方括号
**命令格式**  
`[[ expression ]]`

**新增命令**  
支持模式匹配`[[ $USER == r* ]]`

### `case`命令
**命令格式**
```bash
case variable in
pattern1 | pattern2) command1;;
pattern3) command2;;
*) default commands;;
```

### `for`命令
**命令格式**
```bash
for var in list
do
  commands
done
```

### `while`命令
**命令格式**
```bash
while test command
do
  other commands
done
```

### `until`命令
**命令格式**
```bash
until test commands
do
  other commands
done
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgxNjQ0NjQ5MV19
-->