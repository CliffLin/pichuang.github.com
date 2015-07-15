---
layout: post
title: 'SDN Lab 4$ Mininet Upgrade'
date: 2014-09-03 10:12
comments: true
categories: 
---
mininet 要如何安裝? 這部分 mininet 有給很[詳細介紹](http://mininet.org/download/) 裡面提供的 OpenvSwitch 版本算是非常久遠的, 現在 OpenvSwitch 已經來到 2.3 了, 順應潮流我們也來把 mininet 上的 OpenvSwitch 升級一下

# 安裝過程
## 下載 mininet
```
git clone git://github.com/mininet/mininet && cd mininet
```

## 安裝 mininet 
```
mininet/util/install.sh -a
```
* install everything (using your home directory)

## 升級 Mininet 內 OpenvSwitch (需root權限)
```
wget -O - https://gist.githubusercontent.com/pichuang/9b362f802f40913c4b8f/raw/00973d381f1a6ab7ffaf229b71f2f52314e23894/upgrade_ovs_in_mininet.sh | bash 
```
* 若出現 `Cannot find required executable ovs-controller.` 這是因為 OpenvSwitch 已經把 ovs-controller 掉了, 所以你需要自己找一套 controller 測試

## (Optional) Disable IPv6
- vim /etc/sysctl.d/90-disable-ipv6.conf
```
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
```
  - 避免 mininet hosts 發送 ipv6 封包產生 packet_in
- sysctl -p /etc/sysctl.d/90-disable-ipv6.conf

## 有圖
<img class="center" src="https://lh3.googleusercontent.com/-j_fX6Nyv1kw/VAZ_Xe-P8HI/AAAAAAAAFTw/S4IP3nziFCE/w1033-h802-no/mininet-upgrade.PNG" width="75%" height="75%">

#Reference
- [Installing new version of Open vSwitch](https://github.com/mininet/mininet/wiki/Installing-new-version-of-Open-vSwitch)
- [Download/Get Started With Mininet](http://mininet.org/download/)
- [MiniNet as an SDN test platform](http://www.routereflector.com/2013/11/mininet-as-an-sdn-test-platform/)
- Thanks to @tutul