# 一个执着于 Windows 系统重装/重置的程序猿，如何快速配置必要的开发套件

由于在去年有段时间需要进行一些`Windows`系统的应用开发，于是就手动攒了一台台式机（不要问什么配置，问就是4090），既然电脑有了就有各种各样倒腾系统的过程了。

在使用过`macOS`系统之后，对于自己的`Windows`系统就各种看不顺眼，一天到晚捣鼓捣鼓，三天两头重装系统，因此简单记录一下如何快速构建一套开发套件环境。

## 系统安装与重置

### 重装系统

重装电脑系统的话，首先要下载一个完全纯净版的官方原版系统，建议从良心[`i tell you`](https://next.itellyou.cn/)网站下载，具体的系统版本看个人喜好了。

有了系统之后，需要制作**U盘启动工具**，此处特别建议大家使用[`ventoy`](https://www.ventoy.net/cn/)，这个工具可以在U盘中单独划分一个分区来存放系统镜像，同时还不影响U盘正常功能的使用；同时**Ventoy**还支持引导不同版本的系统，只需要将相应的系统镜像放到U盘中即可。

安装方式也很简单：
1. 安装软件
2. 插上U盘
3. 在U盘中写入`Ventoy`
4. 将下载好的系统镜像放入到U盘中
5. 重启电脑，**BIOS**启动选择U盘启动
6. 进入到下面的页面，就成功了**90%**

![image.png](https://img.pongj.com/f357a49c29b740889d3ebd74ac01bd05~tplv-k3u1fbpfcp-watermark.image)

7. 选择要安装的系统版本，回车
8. 然后就进入到系统的安装界面了，
9. 巴拉巴拉...
10. 安装好了 **:)**

系统安装好了就要激活，作为21世纪的有志（呸呸...）青年，当时是要使用正版的激活码（白眼），此处省略一万字，详细的注（bai）册（piao）方式可以在`Github`中有工具。

比如：[爱发电的勇士1](https://github.com/zbezj/HEU_KMS_Activator)、[爱发电的勇士2](https://github.com/netnr/kms)、[爱发电的勇士3](https://github.com/dylanbai8/kmspro)

实在有搞不定的，请转身**拼夕夕**......

以上一个完全纯净的系统就安装好啦。

### 系统重置

在最新的**Windows10**、**Windows11**系统中，可以选择重置电脑了，可以选择**保留用户文件夹**或者**清理驱动器**，重置之后的系统就是和**崭新出厂**的系统是一样的。

具体的重置步骤为：

1. 打开设置，也可以快捷键（Win + I）

![image.png](https://img.pongj.com/1a4004f2833d4087890a9fe91eefe07f~tplv-k3u1fbpfcp-watermark.image)
2. 打开**恢复**
![image.png](https://img.pongj.com/352bdc0a4c1a49ca8ec1ad6d92a83dfd~tplv-k3u1fbpfcp-watermark.image)
3. 选择**重置此电脑**
4. 选择要重置的选项

然后静静的等待......

## 软件安装

作为一个合格的全栈开发师，安装的软件必须要**简单省事**。

### scoop

一个很不错的软件管理包，可以安装一些二进制软件包，也可以从Github中安装软件包，官网地址[传送门](https://scoop.sh/)

安装方式也很简单，打开PowerShell，粘贴一下命令

```bash
> Set-ExecutionPolicy RemoteSigned -Scope CurrentUser # Optional: Needed to run a remote script the first time
> irm get.scoop.sh | iex
```

安装完成之后，可以使用**scoop**安装`Git`、`Node.js`、`pnpm`、`yarn`、`7zip`等

### Chocolatey

`Chocolatey`也是`Windows`系统中很好用的包管理工具，结合`scoop`一起使用，就有了`macOS`系统中强大的`Homebrew`的使用体验了

安装步骤：

以管理员身份打开`Powershell`，输入以下命令即可

```
iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))
```

![image-20230302074811975](https://img.pongj.com/image-20230302074811975.png)

### Git

建议使用`scoop`安装

```
scoop install git
```

`Git`安装的过程同时会安装`7zip`，安装完成后可以设置`7zip`在右键菜单中使用

1. 打开**工具**
2. 打开**选项**
3. 选择**7-Zip**
4. 勾选**添加7-Zip到右键菜单**

![image-20230302074021890](https://img.pongj.com/image-20230302074021890.png)

### Node.js

使用`scoop`安装`lts`版本即可

```
scoop install nodejs-lts
```

### pnpm

```
scoop install pnpm
```

### Anaconda

使用`Python`开发，建议安装`anaconda`，安装`miniconda`也是可以的

### Visual Studio

安装`Visual Studio`是为了做一些`node-gyp`项目的编译

### Visual Studio Code

宇宙最强编辑器**：）**

## 其他软件

- `Insomnia`：开源的基于`Kong`的接口测试工具，[传送门](https://github.com/Kong/insomnia)
- `snipaste`：好用的截图工具，[传送门](https://www.snipaste.com/)
- `koodo-reader`：好用的开源电子书阅读器，[传送门](https://github.com/troyeguo/koodo-reader)
- `steam`：额，很多快乐的源泉......

- `CloudDriver`：可以把网盘挂在到本地作为本地磁盘使用
- `PotPlayer`：支持`webdav`的播放器，可以直接播放网盘中的资源
- `PicGo`：好用的图床工具

其他一些更好用的也在补充中。