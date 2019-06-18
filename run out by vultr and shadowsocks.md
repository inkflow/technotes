在服务器上搭建Shadowsocks
------
Xshell连上服务器后，逐步输入以下三行指令
```
wget --no-check-certificate -O shadowsocks.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh
```
```
chmod +x shadowsocks.sh
```
```
./shadowsocks.sh 2>&1 | tee shadowsocks.log
```
依次输入以下三个参数
password
port
security->7
