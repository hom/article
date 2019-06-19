# `firewalld`防火墙使用

## 常用命令

### 获取防火墙状态
```bash
$ systemctl status firewalld
# or
$ firewall-cmd --state
```

### 开启、停止防火墙
1. 开启
```bash
$ systemctl start firewalld
# or
service firewalld start
```
2. 停止
```bash
$ systemctl stop firewalld
# or
$ service firewalld stop
```
3. 重新启动
```bash
$ systemctl restart firewalld
# or
$ service firewalld restrat
# or
$ systemctl-cmd reload
```
4. 开机启动
```bash
$ systemctl enable firewalld
```
4. 禁止开机启动
```bash
$ systemctl disable firewalld
```

### 规则修改
1. 开放端口
```bash
# --zone 作用域
# --add-port 添加端口
# --permanent 永久生效，否则重启后失效
$ firewall-cmd --zone=public --add-port=80/tcp --permanent
```
2. 禁用端口
```bash
$ firewall-cmd --zone-public --remove-port=80/tcp --permanent
```
3. 查看所有开放端口
```bash
$ firewall-cmd --list-ports
# 查看所有规则
$ firewall-cmd --list-all
```

#### 其他参数说明
```bash
$ firewall-cmd --state # 查看防火墙状态
$ firewall-cmd --reload # 重新载入配置
$ firewall-cmd --get-zones # 列出支持的zone
$ firewall-cms --get-services # 列出支持的服务，在列表中的服务是放行的
$ firewall-cms --query-service ftp # 查看ftp服务是否支持，返回yes / no
$ firewall-cmd --add-service=ftp # 临时开放ftp服务
$ firewall-cmd --add-service=ftp --permanent # 永久开放ftp服务
$ firewall-cmd --remove-service=ftp --permanent # 永久移除ftp服务
$ firewall-cmd --list-service # 列出开放的服务
$ iptables -L -n # 查看规则，这个命令和iptables命令相同
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkyMDk5NTQ5MF19
-->