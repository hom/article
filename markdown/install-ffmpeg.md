### 安装`EPEL Release`源
> 需要使用第三方`repo`源 
1. 安装`epel-release`
```bash
yum install -y epel-release
```
2. 如果出现缺少`Code`提示
```bash
sudo rpm –import /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
```
3. 查看安装是否成功
```bash
yum repolist
```

### 安装`Nux-Dextop`源
1. 导入`Code`
```bash
sudo rpm –import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro
```
2. 安装`Nux-Dextop`源
```bash
sudo rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-1.el7.nux.noarch.rpm
```
3. 查看`repo`源是否安装成功
```bash
yum repolist
```

### 安装`ffmpeg`
```bash
yum install -y ffmpeg
```