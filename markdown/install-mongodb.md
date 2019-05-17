1. 新建`yum`源。
```bash
$ vim /etc/yum.repos.d/mongodb-org-3.6.repo
```
2. 配置`yum`源内容
```bash
[mongodb-org-3.6]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.6/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.6.asc
```
3. 安装
```bash
sudo yum install -y mongodb-org
```