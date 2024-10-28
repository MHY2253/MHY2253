- 下载程序

```
curl -Lo hysteria https://github.com/apernet/hysteria/releases/latest/download/hysteria-linux-amd64 && chmod +x hysteria && mv -f hysteria /usr/local/bin/
```
- 编写配置文件

```
vim /usr/local/etc/config.yaml
```
写入以下内容
```
# listen: :443 

tls:
  cert: /usr/local/etc/fullchain.pem
  key: /usr/local/etc/private.key 

auth:
  type: password
  password: Se7RAuFZ8Lzg 

bandwidth:
  up: 500 mbps
  down: 500 mbps

ignoreClientBandwidth: false

disableUDP: false

udpIdleTimeout: 60s

masquerade: 
  type: proxy
  proxy:
    url: https://news.ycombinator.com/ 
    rewriteHost: true
```