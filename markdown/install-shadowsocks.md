# shadowsocks搭建

## 安装

### `Python`

#### `PyPi`
1. 查看`python版本`
```bash
# First, make sure you have Python 2.6 or 2.7.
$ python --version
```
2. 查看`pip`
```bash
$ pip --version
# 如果没用则需要安装
$ curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
$ python get-pip.py 
```
3. 安装`shadowsocks`
```bash
$ pip install shadowsocks
```
4. 查看`ssserver`服务
```bash
$ ssserver -h
```

#### GitHub
从[GitHub](https://github.com/shadowsocks/shadowsocks)下载安装
1. `Install`
`Debian`/`Ubuntu`:
```bash
$ apt-get install python-pip
$ pip install git+https://github.com/shadowsocks/shadowsocks.git@master
```
CentOS:
```bash
$ yum install python-setuptools && easy_install pip
$ pip install git+https://github.com/shadowsocks/shadowsocks.git@master

# For CentOS 7, if you need AEAD ciphers, you need install libsodium
# libsodium支持chacha20加密方法
$ dnf install libsodium python34-pip
$ pip3 install  git+https://github.com/shadowsocks/shadowsocks.git@master
```
Linux distributions with snap:
```bash
$ snap install shadowsocks
```
#### 配置文件
```json
{
  "server":"my_server_ip",
  "server_port":8388,
  "local_address": "127.0.0.1",
  "local_port":1080,
  "password":"mypassword",
  "timeout":300,
  "method":"aes-256-cfb",
  "fast_open": false
}
```
说明信息
Name | Explanation
-----|------------
server | the address your server listens
server_port | server port
local_address | the address your local listens
local_port | local port
password | password used for encryption
timeout | in seconds
method | default: "aes-256-cfb", see [Encryption](https://github.com/shadowsocks/shadowsocks/wiki/Encryption)
fast_open | use [TCP_FASTOPEN](https://github.com/shadowsocks/shadowsocks/wiki/TCP-Fast-Open), true / false
workers | number of workers, available on Unix / Linux

#### 使用方法
```bash
# start custome
$ ssserver -p 443 -k password -m aes-256-cfb
# start width deamon
$ sudo ssserver -p 443 -k password -m aes-256-cfb --user nobody -d start
# stop
$ sudo ssserver -d stop
# check the log
$ sudo less /var/log/shadowsocks.log
# If you installed the snap package, you have to prefix the commands with shadowsocks., like this:
$ shadowsocks.ssserver -p 443 -k password -m aes-256-cfb
```

### `Go`
#### 配置文件
```json
{
    "server":"127.0.0.1",
    "server_port":8388,
    "local_port":1080,
    "local_address":"127.0.0.1",
    "password":"barfoo!",
    "method": "aes-128-cfb",
    "timeout":600
}
```
#### GitHub
```bash
# on server
$ go get github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-server
# on client
$ go get github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-local
```
#### 使用
1. 在客户端使用多个服务地址
```bash
$ server_password    specify multiple server and password, server should be in the form of host:port
```
配置文件格式
```json
{
	"local_port": 1081,
	"server_password": [
		["127.0.0.1:8387", "foobar"],
		["127.0.0.1:8388", "barfoo", "aes-128-cfb"]
	]
}
```
2. 在服务端使用多个端口
```bash
$ port_password   specify multiple ports and passwords to support multiple users
```
配置文件格式
```json
{
	"port_password": {
		"8387": "foobar",
		"8388": "barfoo"
	},
	"method": "aes-128-cfb",
	"timeout": 600
}
```

### C with libev

### C++ with Qt

### Perl
