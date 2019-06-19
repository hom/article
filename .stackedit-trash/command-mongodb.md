## Mongodb Shell

### 基本使用
查看数据库并连接到相应的数据库
```bash
$ show dbs
$ use database_name
```

查看表列表
```bash
$ show tables
# or
$ show collections
```

查找数据
```bash
#查找所有数据
$ db.collecion.find()
#查找特定数据
$ db.collection.find({'key': 'value'})
```

更新数据
```bash
#更改字段名字
$ db.collection.update({'key': 'value'}, {$rename: {'old_name': 'new_name'}}, false, true)
#删除字段
$ db.collection.update({'key': 'value'}, {$unset: {'key': ''}}, false, true)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjg0NTk3NzQ1XX0=
-->