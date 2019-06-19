## 安装
```bash
$ yum install -y traceroute
```

## 使用
### 追踪路由
```bash
# -n 是不尝试解析ip的域名，这样会更快。每行结果后面会有3个时间参数，分别代表三次请求的时间
# -i 指定网卡接口
$ traceroute -n -i eth0 www.baidu.com
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbODg2MjU5NDI4XX0=
-->