### 创建容器
#### 新建容器
**命令**`docker create`
```bash
$ docker create -it ubuntu:18.04
d5cf362d68bf1b5763148560ce93f5ff907e5ea9c978e1cf28210f1fa8a5b245
$ docker ps -a 
CONTAINER ID   IMAGE      COMMAND     CREATED   STATUS    PORTS    NAMES
d5cf362d68bf   ubuntu:18.04   "/bin/bash"  16 seconds ago   Created  jovial_bohr
```

**`create`和`run`命令包括几大类**  

- 与容器运行模式相关
- 与容器和环境配置相关
- 与容器资源限制和安全配置相关

1. `create`和容器运行模式相关的选项  

选项     |     说明
--------|---------
`-a`,`--attach=[]` | 是否绑定到标准输入、输出和错误
`-d`,`--detach=true/false` | 是否在后台运行容器，默认为否
`--detach-keys=""` | 从`attact`退出的快捷键
`--entrypoint=""` | 镜像存在入口命令时，覆盖为新的命令
`--expose=[]` | 指定容器会暴露出来的端口或端口范围
`--group-add=[]` | 运行容器的用户组
`-i`,`--interactive=true/false` | 保持标准输出打开
`--ipc=""` | 容器`IPC`命名空间，可以为其它容器或主机
`--isolation="default"` | 容器使用隔离机制
`--log-drive="json-file"` | 指定容器的日志驱动类型
`--log-opt=[]` | 传递给日志驱动的选项
`--net="bridge"` | 指定容器网络模式
`--net-alias=[]` | 容器在网络中的别名
`-P`, `--publish-all=true/false` | 通过`NAT`机制将容器暴露的端口自动映射到本地主机的临时端口
`-p`, `--publish=[]` | 指定端口如何映射到主机端口。例如`-p 11234-12234:1234-2234`
`--pid` | 容器的`PID`命名空间
`--userns=""` | 启用`userns-remap`时配置用户命名空间的模式
`--uts=host` | 容器的`UTS`命名空间
`--restart="no"` | 容器的重启策略，
`--rm=true/false` | 容器退出后是否自动删除，默认为`false`
`-t`,`--tty=true/false` | 是否分配一个伪终端，默认为`false`
`--tmpfs=[]` | 挂载临时文件系统到容器
`-v`,`--volume[=[[HOST-DIR:]CONTAINER-DIR[:OPTIONS]]]` | 挂载主机上的文件卷到容器内
`--volume-driver=""` | 挂在文件卷的驱动类型
`--volumes-from=[]` | 从其他容器挂载卷
`-w`,`--workdir=""` | 容器内的默认工作目录


2. `create`与容器环境和配置相关的选项

选项    |     说明
-------|--------
`--add-host=[]` | 在容器内添加一个主机名到`IP`地址的映射关系（通过`/etc/hosts`文件）
`--device=[]` | 映射物理机上的设备到容器内
`--dns-search=[]` | `DNS`搜索域
`--dns-opt=[]` | 自定义的`DNS`选项
`--dns=[]` | 自定义的`DNS`服务器
`-e`,`--env=[]` | 指定容器内环境变量
`--env-file=[]` | 从文件内读取环境变量到容器内
`-h`,`--hostname=""` | 指定容器内的主机名
`--ip=""` | 指定容器内的`IPv4`地址
`--ip6=""` | 指定容器内的`IPv6`地址
`--link-[<name or id>:alias]` | 链接到其他容器
`--mac-address` | 指定容器的`MAC`地址
`--name` | 指定容器的别名

3. `create`与容器资源限制和安全保护相关的选项

选项    |    说明
-------|--------
`--blkio-weight=10~1000` |

#### 新建并启动容器
`docker run` == `docker create` + `docker start`
`ctrl + d` 或者`$ exit`退出容器
**错误代码**  

- `125` `Docker daemon`执行出错。比如执行了不支持的`Docker`命令参数
- `126` 所有命令无法执行。比如权限出错
- `127` 容器内命令无法找到

#### 终止容器

`docker stop [-t|--time[=10]][CONTAINER...]`
首先向容器发送`SIGTERM`信号，等待一段时间（默认10秒），再发送`SIGKILL`终止容器
`docker kill`
直接发送`SIGKILL`终止容器

#### 进入容器
1. `attach`命令
`docker attach [--detach-keys[=[]] [--no-stdin] [--sig-proxy[=true]] CONTAINER`

- `--detach-keys[=[]]` 指定退出`attach`模式的快捷键，默认是`ctrl+p`或`Ctrl+q`
- `--no-stdin=true/false` 是否关闭标准输入，默认保持打开
- `-sig-proxy=true/false` 是否代理收到的系统信号给应用进程，默认为`true`

2. `exec`命令
`docker exec [-d|--detach] [--detach-keys[=[]]] [-i|--interactive] [--privileged] [-t|--tty] [-u|--user[=USER]] CONTAINER COMMAND [ARG...]`

3. `nsenter`命令
首先需要找到容器进程额`PID`
`PID=$(docker inspect --format "{{ .State.Pid }}" <container>)`
通过`PID`连接到容器
`$ nsenter --target $PID --mount --uts --ipc --net --pid`

### 删除容器
`docker rm[-f|--force][-l|--link][-v|--volumes]CONTAINER[CONTAINER...]`  

- `-f`,`--force=false` 是否强行进入并删除一个运行中的容器
- `-l`,`--link=false` 删除容器的连接，但保留容器
- `-v`,`--volumes=false` 删除容器挂载的数据卷

### 导入和导出容器
#### 导入容器
`docker import [-c|--change=[=[]]] [-m|--message[=MESSAGE]] file|URI|_[REPOSITORY[:TAG]]`
#### 导出容器
`docker expoert[-o|--output[=""]]CONTAINER`