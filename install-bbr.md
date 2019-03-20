# CentOS开启BBR加速

## 查看
查看内核版本
```bash
$  uname -a
Linux vultr.guest 4.19.8-1.el7.elrepo.x86_64 #1 SMP Sat Dec 8 10:07:47 EST 2018 x86_64 x86_64 x86_64 GNU/Linux
```

## 升级
1. 安装`eprl`源
```bash
$ sudo rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
$ sudo rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm
```
2. 安装最新的内核版本
```bash
$ sudo yum --enablerepo=elrepo-kernel install kernel-ml -y
```
3. 查看系统现在所有的内核
```bash
$ rpm -qa | grep kernel
```
4. 修改`grub2`的启动项，设置启动之后选择最新的内核
```bash
$ sudo egrep ^menuentry /etc/grub2.cfg | cut -f 2 -d \'
$ sudo grub2-set-default 0 # 设置第一个为默认启动项
```
5. 重启机器
```bash
$ sudo reboot
```

## 开启BBR

### 一键安装脚本
```bash
$ sudo wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && ./bbr.sh
```