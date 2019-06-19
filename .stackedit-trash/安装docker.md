# 安装docker

## 安装

### centos
#### 包安装
卸载旧版本
```bash
$ sudo yum remove docker \
docker-common \
docker-selinux \
docker-engine
```
安装依赖包
```bash
$ sudo yum install yum-utils \
device-mapper-persistent-data \
lvm2
```
添加`yum源`
```bash
# 官方源
# $ sudo yum-config-manager \
#--add-repo \
#https://download.docker.com/linux/centos/docker-ce.repo

# 建议使用国内源
$ sudo yum-config-manager \
--add-repo \
https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

```

安装最新版本的`docker-ce`
```bash
$ sudo yum-config-manager --enable docker-ce-edge
```

安装测试版本的`docker-ce`
```bash
$ sudo yum-config-manager --enable docker-ce-test
```

安装`docker-ce`
```bash
$ sudo yum makecache fast
$ sudo yum install docker-ce
```

### 通过脚本安装
```bash
$ curl -fsSL https://get.docker.com/ | sh
# or
$ wget -qO- https://get.docker.com/ | sh
```

## 配置镜像加速
### linux
```bash
$ curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s http://f1361db2.m.daocloud.io
```

### macos
右键点击桌面顶栏的 docker 图标，选择 Preferences ，在 Daemon 标签（Docker 17.03 之前版本为 Advanced 标签）下的 Registry mirrors 列表中加入下面的镜像地址:
```bash
$ http://f1361db2.m.daocloud.io
```

### 配置完成后重启`docker`即可生效
```bash
$ sudo systemctl restart docker
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTcxMTM3NjAxN119
-->