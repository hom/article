### 获取镜像
`docker pull [选项] [Docker Registry 地址[:端口号]/]仓库名[:标签]`

- `NAME` 是镜像仓库的名称（用来区分镜像）
- `TAG` 是镜像的标签（用来表示版本信息）

*子命令参数*  
`-a`或者`--all-tags=true/false`是否获取仓库中所有镜像，默认`false`

示例：
```bash
# 获取Ubuntu版本，如果不指定TAG默认获取latest
$ docker pull ubuntu:18.04
18.04: Pulling from library/ubuntu
32802c0cfa4d: Pull complete
da1315cffa03: Pull complete
fa83472a3562: Pull complete
f85999a86bef: Pull complete
Digest: sha256:6d0e0c26489e33f5a6f0020edface2727db9489744ecc9b4f50c7fa671f23c49
Status: Downloaded newer image for ubuntu:18.04

```

### 查看镜像信息
**列出镜像** `docker images`  
```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              18.04               93fd78260bd1        10 days ago         86.2MB
hello-world         latest              4ab4c602aa5e        2 months ago        1.84kB
```

**使用`tag`镜像添加标签**
```bash
$ docker tag ubuntu:18.04 nuoooo:ubuntu
```

**使用`inspect`查看镜像详细信息**
```bash
$ docker inspect ubuntu:18.04
# 具体信息
...
```

**使用`history`查看镜像历史**

- 使用`--no-turnc`命令输出完整命令

```bash
$ docker history ubuntu:18.04
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
93fd78260bd1        10 days ago         /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B
<missing>           10 days ago         /bin/sh -c mkdir -p /run/systemd && echo 'do…   7B
<missing>           10 days ago         /bin/sh -c rm -rf /var/lib/apt/lists/*          0B
<missing>           10 days ago         /bin/sh -c set -xe   && echo '#!/bin/sh' > /…   745B
<missing>           10 days ago         /bin/sh -c #(nop) ADD file:39e5bc157a8be63bb…   86.2MB
```

### 搜寻镜像  

- `--automated=true/false`仅显示自动创建的惊醒，默认为`false`
- `--no-turnc=true/false`输出信息不截断显示，默认为`false`
- `-s` `--stars=X`指定仅显示评价为星级以上的镜像，默认为0

```bash
$ docker search centos
```

### 删除镜像
**命令**`docker rmi IMAGE[IMAGE...]`  

- `IMAGE`可以为标签或者`ID`

```bash
# 删除nuoooo:ubuntu镜像
$ docker rmi nuoooo:ubuntu
Untagged: nuoooo:ubuntu
```

### 创建镜像
#### 基于已有镜像的容器创建
`docker commit [OPTIONS]CONTAINER[REPOSITORY[:TAG]]`  
- `-a` `--author=""`作者信息
- `-c` `--change=[]` 提交的时候执行的`Dockerfile`命令，包括`CMD`|`ENTERPOINT`|`ENV`|`EXPOSE`|`LABEL`|`ONBUILD`|`USER`|`VOLUME`|`WORKDIR`
- `-m` `--message=""`提交的信息
- `-p` `--pause=true` 提交时暂停容器运行

#### 基于本地模板导入
`docker import [OPTIONS]file|URL|-[REPOSITORY[:TAG]]`
#### 基于`Dockerfile`创建

### 存出和载入镜像
`docker save`和`docker load`实现镜像存出和载入