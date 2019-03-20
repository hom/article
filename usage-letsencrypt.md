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