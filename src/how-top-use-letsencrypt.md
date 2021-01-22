在做 Web 开发中，对网站内容的基本安全加密就是使用 HTTPS，并且在一些重视安全性的软件中，HTTPS 必不可少，微信开发中配置的域名强制使用 HTTPS，`parse-dashboard` 的配置连接必须使用 HTTPS，等等。

现在可以很方便的在各云服务提供商购买证书，唯一的缺点就是需要 **付费**，那么有没有 **免费**、**白嫖** 的证书呢？

答案是 **有的**，今天介绍的就是使用比较知名的自签名证书机构 Letsencrypt 来对自己的网站域名签发证书了支持 HTTPS。

1. 登录到服务器

   使用 `ssh` 登录到运行的网站的服务器。

2. 安装 `snapd`

   `snapd` 是目前各个 `Linux` 发行版中很好用的包管理工具。

   示例中的安装是基于 `CentOS 7` 系统来安装的，如果你使用的是其他发行版的系统，那么具体的安装请参考 `snapd` 的官网中的安装文档，[传送门](https://snapcraft.io/docs/installing-snapd)。

   - 添加 REPL 

     - CentOS 8

       ```bash
       $ sudo dnf install epel-release
       $ sudo dnf upgrade
       ```

       

     - CentOS 7

       ```bash
       $ sudo yum install epel-release
       ```

       

   - 安装 `snapd`

     - 配置了 REPL 之后，输入下面命令即可安装 `snapd` 

       ```bash
       $ sudo yum install snapd
       ```

     - 安装完成后，`systemd` 服务需要执行 `enable`

       ```bash
       $ sudo systemctl enable --now snapd.socket
       ```

     - 将 `snapd` 的文件目录链接到系统的路径中

       `snapd` 安装完成之后提供的命令是 `snap`， 默认安装在 `/snap` 的目录中

       ```bash
       $ sudo ln -s /var/lib/snapd/snap /snap
       ```

       

3. 查看 `snapd` 版本

   执行命令安装 `snapd` 核心库，确保安装的 `snapd` 版本是最新的。

   ```bash
   sudo snap install core; sudo snap refresh core
   ```

4. 移除 `certbot-auto` 和其他 Certbot 模块包

   使用不同系统自身的包管理工具卸载已经安装的 Certbot 模块，常用的 `apt` `yum` `dnf` 等。

   ```bash
   sudo apt-get remove certbot, sudo dnf remove certbot, or sudo yum remove certbot
   ```

5. 安装 Certbot

   Certbot 是生成 HTTPS 证书的主要工具，在之前的版本中 Certbot 使用 Python 来安装，由于 Python 中安装包总是出现版本不一致的问题导致安装不成功，因此官方建议现在使用 `snap` 来安装 Certbot。

   ```
   sudo snap install --classic certbot
   ```

6. 将 certbot 链接到系统环境变量中

   ```
   sudo ln -s /snap/bin/certbot /usr/bin/certbot
   ```

7. 使用 Nginx 生成 HTTPS 证书

   使用 Nginx 生成证书有两种方式：

   - 使用 `certbot` 生成证书并且使用 `certbot` 更改 Nginx 的配置文件

     ```bash
     sudo certbot --nginx
     ```

   - 仅使用 `certbot` 生成证书

     ```bash
     sudo certbot certonly --nginx
     ```

   在生成证书的过程中，`certbot` 会提示你输入邮箱来进行下一步的验证，此时你可以在执行命令的时候添加 `--register-unsafely-without-email` 跳过邮箱验证步骤：

   ```bash
   sudo certbot --nginx --certonly --register-unsafely-without-email
   ```

   然后在接下来的步骤中根据要生成证书的域名选择就可以生成自己的 HTTPS 证书啦

8. 配置自动更新证书

   由于 Letsencrypt 提供的证书的有效期只有 `90` 天，所以我们需要对我们的证书及时续签。

   通过执行 `renew` 命令来进行证书续签操作，添加 `--dry-run` 参数代表模拟续签，查看执行命令的结果输出

   ```bash
   sudo certbot renew --dry-run
   ```

9. 使用 `crontab` 添加定时续签

   在 `Linux` 执行定时任务，离不开使用 `crontab` 命令，在 `crontab` 配置中添加以下配置

   ```bash
   0 0,12 * * * sudo certbot renew > /var/log/certbot.renew.log
   ```

   以上脚本代表在每天的 24 点和 12 点定时检查证书是否到期，并执行续签操作。

10. 查看 HTTPS 服务是否正确开启

   - 在浏览器中打开配置 HTTPS 的域名，查看是否已经切换成了 HTTPS 的标志

   - 在命令行中通过 `curl` 命令查看 HTTPS 是否开启

     在命令行中输入以下命令查看域名的输出：

     ```bash
     curl -vIL https://zi.pongj.com
     ```

     输出结果中，可以看到配置的 HTTPS 证书信息，证书的签署日期是 `Dec 29 07:06:07 2020 GMT`，到期日期是 `Mar 29 07:06:07 2021 GMT`

     ```bash
     * About to connect() to zi.pongj.com port 443 (#0)
     *   Trying 49.235.105.234...
     * Connected to zi.pongj.com (49.235.105.234) port 443 (#0)
     * Initializing NSS with certpath: sql:/etc/pki/nssdb
     *   CAfile: /etc/pki/tls/certs/ca-bundle.crt
       CApath: none
     * SSL connection using TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
     * Server certificate:
     * 	subject: CN=zi.pongj.com
     * 	start date: Dec 29 07:06:07 2020 GMT
     * 	expire date: Mar 29 07:06:07 2021 GMT
     * 	common name: zi.pongj.com
     * 	issuer: CN=R3,O=Let's Encrypt,C=US
     > HEAD / HTTP/1.1
     > User-Agent: curl/7.29.0
     > Host: zi.pongj.com
     > Accept: */*
     >
     < HTTP/1.1 200 OK
     HTTP/1.1 200 OK
     < Server: nginx/1.18.0
     Server: nginx/1.18.0
     < Date: Fri, 22 Jan 2021 05:40:37 GMT
     Date: Fri, 22 Jan 2021 05:40:37 GMT
     < Content-Type: text/html; charset=utf-8
     Content-Type: text/html; charset=utf-8
     < Content-Length: 219958
     Content-Length: 219958
     < Connection: keep-alive
     Connection: keep-alive
     < ETag: "35b36-TbUTbYgQ6yT1OJeOQSyX0F3IN9g"
     ETag: "35b36-TbUTbYgQ6yT1OJeOQSyX0F3IN9g"
     < Accept-Ranges: none
     Accept-Ranges: none
     < Vary: Accept-Encoding
     Vary: Accept-Encoding
     
     <
     * Connection #0 to host zi.pongj.com left intact
     ```

     