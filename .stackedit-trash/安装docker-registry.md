# docker搭建私有仓库

## 安装docker
> 可以按照文档安装`docker`

## 安装`registry`仓库

1. 下载`registry`镜像
```bash
$ docker pull registry
```

2. 启动`registry`
```bash
# -d 以服务运行
# -p 端口映射
# --restart 在容器退出时总是重启容器,主要应用在生产环境
# -v 默认情况下，会将仓库存放于容器内的/var/lib/registry目录下，指定本地目录挂载到容器
$ docker run -d -p 5000:5000 --name registry --restart=always -v /opt/registry:/var/lib/registry registry:latest
```

3. 查看仓库
```bash
$ docker ps
```

4. 验证仓库
```bash
$ curl hub.nuoooo.com/v2/_catalog
{"repositories":[]}
```

## 仓库使用

1. 配置
> `dockers registry V2` 版本客户端默认使用`https`协议去`push`镜像到仓库服务器，而现在我们的仓库服务器只配置了支持`http`，所以客户端会`push`镜像失败。如要希望`docker`客户端支持`http`协议，需在启动`docker`时加入参数`--insecure-registry your_registry_ip:port `

在`/usr/lib/systemd/system/docker.service`中添加`--insecure-registry hub.nuoooo.com`
```bash
ExecStart=/usr/bin/dockerd -H unix:// --insecure-registry hub.nuoooo.com
ExecReload=/bin/kill -s HUP $MAINPID
```

3. 为提交到的镜像添加标签
```bash
$ docker tag ubuntu:18.04 hub.nuoooo.com/ubuntu:18.04
```
2. 推送到仓库
```bash
$ docker push hub.nuoooo.com/ubuntu:18.04
```
**Note**   
- 如果仓库使用的是`nginx`,可能会由于`nginx`的上传文件大小限制而报错,在`nginx`配置文件`http`块或者`server`块添加`client_max_body_size 20m;`

3. 查看仓库
```bash
$ ls /opt/registry/docker/registry/v2/repositories
hello-world  ubuntu
```
4. 拉取镜像
```bash
$ docker pull hub.nuoooo.com/ubuntu:18.04
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAzMDczMTg3M119
-->