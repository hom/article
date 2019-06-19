1. 添加`yum`源。新建`/etc/yum.repos.d/nginx.repo`，内容如下：
```bash
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/7/$basearch/
gpgcheck=0
enabled=1
```
2. 执行安装命令
```bash
yum install nginx
```
3. 查看`nginx`版本
```bash
#查看nginx版本
nginx -v
#查看编译参数
nginx -V
```
4. 查看安装目录
```bash
rpm -ql nginx
```
5. 查看配置文件
```bash
# 用于日志切割
/etc/logrotate.d/nginx
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI5NTU1MDA5NV19
-->