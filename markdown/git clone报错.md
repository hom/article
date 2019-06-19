## `git clone`报错解决
### 报错信息
```bash
$ git clone ssh://mengjun@10.0.192.51:29418/groupM
Cloning into "groupM"...
Unable to negotiate with 10.0.192.51 port 29418: no matching key exchange method found. There offer: diffie-hellman-group1-sha1
fetal: Could not read from remote repository.



Please make sure you have the correct access rights and the repository exists.
```
**报错原因：** 表示本机的`git`版本高于服务器`git`版本
### 解决办法
1. 新建配置文件`~/.ssh/config`
```bash
Host 10.0.192.51 # 代码服务器地址
Port 8081 # 端口
KexAlgorithms +diffie-hellman-group1-sha1 #兼容服务器git版本
```
2. 再次执行`git clone`即可
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjEyMjA0MTAyXX0=
-->