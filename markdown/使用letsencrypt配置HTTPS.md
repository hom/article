# 使用`letsencrypt`配置HTTPS

## 安装

```bash
yum install certbot -y
```

## 获取证书

### 如果有网站根目录
```bash
certbot certonly --webroot -w /var/www/example -d example.com -d www.example.com
```
> 这个命令会在`example.com`和`www.example.com`这两个域名生成一个证书，使用`--webroot`模式会在`/var/www/example`中创建`.well-known`文件夹，这个文件夹中包含了一些验证文件，`certbot`会通过访问`example.com/.well-known/acme-challenge` 来验证域名是否绑定的这个服务器

### 如果单独生成
```bash
certbot certonly --standalone -d example.com -d www.example.com
# 接下来会提示输入加密的邮箱
# 如果不想输入邮箱可以添加 --register-unsafely-without-email
certbot certonly --standalone --register-unsafely-without-email -d example.com -d www.example.com
```
> 证书生成后，在`/etc/letsencrypt/live/`目录中看到相应域名的文件夹

### 报错
#### `python-urllib3`
> `failed: python-urllib3.noarch 0:1.10.2-5.el7` //python-urllib3安装失败
```bash
sudo yum update // 升级yum
sudo yum install httpd firewalld mod_ssl openssl epel-release certbot //安装各种依赖

sudo yum install python-urllib3
```
或者下面报错
```bash
Failed:
python-urllib3.noarch 0:1.10.2-5.el7

Complete!
```
需要执行
```bash
sudo pip uninstall urllib3
sudo yum install python-urllib3
```

#### `pyopenssl`
> `ImportError: ‘pyOpenSSL’ module missing required functionality` // 缺少pyOpenSSL模块 

需要执行
```bash
yum install http://cbs.centos.org/kojifiles/packages/pyOpenSSL/16.2.0/3.el7/noarch/python2-pyOpenSSL-16.2.0-3.el7.noarch.rpm
```

#### `module`
> `AttributeError: 'module' object has no attribute 'pyopenssl'` 

需要执行
```bash
pip install requests==2.6.0
easy_install --upgrade pip
```

## 配置

### Nginx配置HTTPS

#### 只配置HTTPS
```bash
server {
    server_name example.com www.example.com;
    listen 443;
    ssl on;
    ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate /etc/letsencrypt/live/example.com/privkey.pem;
    
    location / {
        # ...
    }
}

```

#### 配置HTTP转HTTPS
```bash
server {
    server_name example.com www.example.com;
    listen 80;
    
    rewrite ^/(.*) https://$server_name$1 permanent;
}
```

## 更新证书

### 命令
```bash
certbot renew --dry-run
```

### 添加到crontab
```bash
15 2 * */2 * certbot renew --pre-hook "service nginx stop" --post-hook "service nginx start"
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzE2MDE4NDY1XX0=
-->
