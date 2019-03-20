# ssh使用key登录禁止使用密码

## 生成key

### 使用本机公钥
将本机的`~/.ssh/id_rsa.pub`上传的服务器`~/.ssh/authorized_keys`
```bash
$ scp -P 2222 root@167.179.92.167:~/.ssh/authorized_keys
```

### 服务器生成
1. 生成秘钥
```bash
$ ssh_keygen -t rsa
# 生成的秘钥保存在~/.ssh/目录下
$ ls ~/.ssh/
id_rsa id_rsa.pub
```
2. `sshd`默认使用`.ssh/authorized_key`命名的文件
```bash
$ cat id_rsa.pub >> authorized_keys
```
3. 将私钥保存到本地，并在服务器删除私钥

## 配置
1. 使用`public key`登录
```bash
$ vim /etc/ssh/sshd_config
```
2. 修改一下配置
```bash
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
```
3. 重启服务
```bash
$ systemctl restart sshd
# or 
service sshd restart
```

## 禁用密码登录
修改`/etc/ssh/sshd_config`
```bash
# 修改内容
PasswordAuthentication yes
# 修改为
PasswordAuthentication no
```