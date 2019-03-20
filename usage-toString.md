### Number.prototype.toString()
> toString() 方法返回指定 Number 对象的字符串表示形式。

#### 用法
> numObj.toString([radix])

##### 参数

###### `redix`
指定要用于数字到字符串的转换的基数（从2到36）。如果未指定 `redix` 参数，则默认值为10  

##### 异常信息

###### `RangeError`
如果`toString()` 的`redix` 参数不在2到36之间，则会抛出`RangeError`