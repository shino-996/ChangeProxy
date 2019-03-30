平时在寝室用路由器挂 shadowsocks, 电脑不设置代理, 出门时电脑上开代理, 所以有了切换网络代理设置的需求. 直接用系统的网络位置会断一下网, 很不爽, 于是就有了这个 workflow. 会修改当前所有活跃 network service 的代理.

# 原理

就是用了`networksetup`这个命令:

```sh
# 打开PAC代理
networksetup -setautoproxyurl Wi-Fi http://127.0.0.1:80/whitelist.pac

# 关闭PAC代理
networksetup -setautoproxystate Wi-Fi off

# 打开SOCKS5代理
networksetup -setsocksfirewallproxy Wi-Fi localhost 1080 off

# 关闭SOCKS5代理
networksetup -setsocksfirewallproxystate Wi-Fi off

# 查看PAC代理是否打开
networksetup -getautoproxyurl Wi-Fi

# 查看SOCKS5代理是否打开
networksetup -getsocksfirewallproxy Wi-Fi
```

# 使用方法

首先, 到release中下载workflow文件, 导入到Alfred并编辑.

PAC文件路径和SOCKS5代理IP, 端口也要修改.

# Alfred命令

- pacon
打开PAC代理

- pacoff
关闭PAC代理

- sockson
打开SOCKS5代理

- socksoff
关闭SOCKS5代理

- listproxy
查看PAC、SOCKS5代理情况
