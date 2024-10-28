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
- 编写systemd文件
```
vim /etc/systemd/system/hysteria.service
```
写入以下内容
```
[Unit]
After=network.target nss-lookup.target

[Service]
User=root
WorkingDirectory=/root
CapabilityBoundingSet=CAP_NET_ADMIN CAP_NET_BIND_SERVICE
AmbientCapabilities=CAP_NET_ADMIN CAP_NET_BIND_SERVICE
ExecStart=/usr/local/bin/hysteria server -c /usr/local/etc/config.yaml --log-level debug
Restart=on-failure
RestartSec=10
LimitNPROC=512
LimitNOFILE=infinity

[Install]
WantedBy=multi-user.target
