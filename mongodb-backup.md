## MongoDB备份

### 导出

#### 命令格式

`mongoexport [OPTIONS]`

#### 命令参数

- `-h` 主机
- `--port` 端口
- `-u username` 用户名
- `-p password` 密码
- `-d` 库名
- `-c` 表名。必填的参数，只有存在的表明才有可能导出数据
- `-f [FIELD[FIELD]]` 列名字
- `-q` 查询条件
- `-csv` 导出`csv`格式数据
- `-o` 导出文件名

### 导入

#### 命令格式

`mongoimport [OPTIONS]`

#### 命令参数
参数基本和`mongoexport`一致，额外的参数如下：

- `--type` 文件类型
- `--file` 文件

### 备份
> 备份的是二进制文件，效率高，连索引信息一起备份出来了。
> 每个`collection`备份出两个文件，一个是二进制`.bson`格式的数据文件，`.json`格式的索引文件。
#### 命令格式
`mongodump [OPTIONS]`
#### 命令参数
命令参数和`mongoexport`一致

### 备份恢复
> 恢复二进制文件到指定数据库  效率高
#### 命令格式
`mongorestore [OPTIONS]`
#### 命令参数
命令和`mongoimport`一致