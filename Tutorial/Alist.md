## 在软路由上部署

> ### 下载程序安装包
```
wget https://github.com/alist-org/alist/releases/download/v3.35.0/alist-linux-musl-x86_64.tar.gz 
```
> ### 进到到 /usr/bin 目录
```
cd /usr/bin
```
> ### 解压、删除程序安全包
```
tar -zxvf alist-linux-musl-x86_64.tar.gz && chmond +x alist && rm alist-linux-musl-x86_64.tar.gz -y
```
> ### 设置密码
```
./alist admin set password
```
> ### 创建开机启动脚本
```
vim /etc/init.d/alist
```
写入以下内容
```
#!/bin/sh /etc/rc.common
START=99
start() {
    cd /usr/bin #alist的路径
    ./alist server #启动alist
}
stop() {
    killall alist
}
```
> ### 赋予脚本执行权限
```
chmod +x /etc/init.d/alist
```
> ### 启动脚本
```
/etc/init.d/alist enable --now
```
