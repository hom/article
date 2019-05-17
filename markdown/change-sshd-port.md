# 更改`ssh`默认`22`端口

## 查看

1. 查看防火墙是否启动

```bash
# centos7使用firewalld
systemctl status firewalld # service firewalld status

# 使用iptables
systemctl status iptables # service iptables status
```

2. 查看`sshd`默认端口

```bash
cat /etc/ssh/sshd_config | grep Port
#Port 22
```

## 设置

1. 打开`/etc/ssh/sshd_config`文件

```bash
vim /etc/ssh/sshd_config
```

2. 在`#Port 22`一行注释去掉，更改为`Port 2222`

3. 修改防火墙规则

```bash
# 简单配置
firewall-cmd --permanent --add-port=2222/tcp
# 添加ip限制，或者拒绝规则
firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="101.254.208.162" port protocol="tcp" port="2222" accept"
```

4. 重启防火墙

```bash
systemctl restart firewalld
# iptables
systemctl restart iptables
```

5. 重启sshd服务

```bash
systemctl restart sshd
```