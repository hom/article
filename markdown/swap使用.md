# swap使用

## 新建

1. 使用`dd`命令创建`swapfile`的`swap`交换文件
```bsh
$ dd  if=/dev/zero  of=/var/swapfile  bs=1024  count=2097152
# or
$ dd if=/dev/zero of=/var/swapfile bs=1024 count=2048k
```
2. 对交换文件格式化为`swap分区`
```bash
$ mkswap /var/swapfile
```
3. 挂在并激活分区
```bash
$ chmod -R 600 /var/swapfile
$ swapon /var/swapfile
```
4. 设置开机自动挂载分区
```bash
$ echo  "/var/swapfile   swap  swap  defaults  0  0" >>  /etc/fstab 
```

## 删除
1. 停止正在使用的分区
```bash
$ swapoff /var/swapfile
```
2. 删除分区文件
```bash
$ rm -rf /var/swapfile
```
3. 删除或者注释掉`/etc/fstab`里设置的开机挂在分区配置
```bash
# /var/swapfile   swap  swap  defaults  0  0
```

## 更改`swap`配置
> swappiness值（0-100），系统对swap分区的依赖程度，越高则越倾向于使用swap分区。
当然，高度依赖swap会造成物理内存远未使用完，就使用swap分区，我们知道swap分区性能远不如物理内存，这反而降低了系统性能，违背了我们创建swap分区的初衷。
我们希望在物理内存即将满荷时再使用swap，这就决定了swappiness值一般为10-60为宜，固态硬盘可以偏高些。
查看当前的swappiness数值：

1. 查看`swappiness`值
```bash
$ cat /proc/sys/vm/swappiness
```
2. 修改`swapiness`值
```bash
$ systemctl vm.swappinexx=50
```
3. 若希望vm.swappiness=50永久生效，则需要修改sysctl配置文件，直接echo追加配置内容，重启系统后即可生效
```bash
$ echo "vm.swappiness = 50"  >>  /etc/sysctl.conf
```

## 增加`swap`分区大小
> 和新建`swap`一样
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MTc5Nzg0NjZdfQ==
-->