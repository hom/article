# 使用`letsencrypt`配置HTTPS

## 安装

```bash
yum install -y certbot python2-certbot-nginx
```

## 获取证书

```bash
sudo certbot certonly --nginx
# 接下来会提示输入加密的邮箱
# 如果不想输入邮箱可以添加 --register-unsafely-without-email
sudo certbot certonly --nginx --register-unsafely-without-email
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
