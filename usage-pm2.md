# pm2设置开机自启动

## 原理
`pm2`作为管理程序监视并自动重启`node`应用，但是`pm2`本身不是作为服务运行，在重启后不能自动运行

## 设置
1. 运行`pm2 startup`会将`pm2`生成`service`服务, 即在`/etc/init.d/`目录下生成`pm2-root`的启动脚本，且自动将`pm2-root`设为服务
```bash
$ pm2 startup
```
2. 运行`pm2 save`会将当前`pm2`所运行的应用保存在`/root/.pm2/dump.pm2`下，当开机重启时，运行`pm2-root`服务脚本，并且到`/root/.pm2/dump.pm2`下读取应用并启动
```bash
pm2 save
```
3. 查看服务状态
```bash
$ systemctl status pm2-root
# or
$ service pm2-root status
```