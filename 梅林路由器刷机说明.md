## 梅林固件

### 一、说明及下载

目的：刷机为带软件中心的梅林版本(目前使用官改)

1. 官方固件刷成原版梅林固件(开始操作错误)

原版梅林为国外RMerl大神基于华硕官方固件源代码修改而来的[梅林固件](https://asuswrt.lostrealm.ca/)

AC86U下载地址：https://koolshare.cn/thread-139965-1-1.html#38481351

AC88U下载地址（[380.70_0-X7.9版本，软件中心使用有问题](http://192.168.49.1/Advanced_FirmwareUpgrade_Content.asp)）：<http://firmware.koolshare.cn/Koolshare_Merlin_Legacy_380/ASUS/RT-AC88U/X7.9/>

AC88U下载地址2(新版本待软件中心)：<https://koolshare.cn/forum.php?mod=viewthread&tid=30748

>AC88U的shadowsocks版本(地址中有多个机型，但AC86U版本不是最新)<https://shadowsocksrr.blogspot.com/2019/04/koolsharessshadowsocks.html>
>
><github最新版本下载：https://github.com/hq450/fancyss_history_package/blob/master/fancyss_arm384/shadowsocks_1.0.4.tar.gz>

登录后可下载带koolshare软件中心的版本

最终刷机版本为：RT-AC86U_384.14_2

2. 原版梅林刷成官改

   升级版本为：RT-AC86U_384_81351_koolshare_cferom_ubi-20191123.w

   1) 在原产固件/原版梅林固件升级页面下直接上传.w 后缀的官改固件文件；

   2) 刷机完成后会自动重启，此时刷机完成（刷机完成后可以不恢复出产设置，当然恢复一次更好）；

   3) 重启后先将路由器连上网络，然后进入软件中心将软件中心更新到最新版本；可使用Ctrl+F5刷新浏览器缓存；

   **默认账号密码：**


### 创建虚拟内存

1. 使用PC上的工具，将U盘格式化为Ext4（这里仅提供Windows版本）

64位：https://pan.baidu.com/s/1JxkE1_SN-4Bh6vx75gHtCQ【提取码: 1ytx】，蓝奏：https://www.lanzous.com/i3qd91c

2. U盘插入到路由器上；
3. 使用软件中心的虚拟内存，将该U盘挂载；

### 安装shadowsocks服务

1. 下载shadowsocks服务：

**科学上网离线安装包（仅适用于RT-AC86U/GT-AC5300/RT-AX88U/GT-AX11000等型号）**[下载地址1](https://raw.githubusercontent.com/hq450/fancyss_history_package/master/fancyss_hnd/shadowsocks_1.7.0.tar.gz) [下载地址2](https://www.lanzous.com/i74cosf)

2. 离线安装

   软件中心->离线安装-》上传并安装：shadowsocks_1.8.1.tar.gz

   这里需要确保剩余空间足够；

3. 也可在github上下载，版本更新

   <https://github.com/hq450/fancyss_history_package/tree/master/fancyss_hnd>

4. 加密方式

   **推荐的混淆obfs：首选http、次选tls**

5. 

### 节点

<https://www.dotunnel005.com/user/node>

使用ssr和v2ray订阅节点

ssr订阅地址：
https://www.plmb001.com/link/2ztHQRolCVeBL9un?mu=0

v2ray订阅地址：
https://www.plmb001.com/link/2ztHQRolCVeBL9un?mu=2

quantumult专用 v2ray订阅地址：
https://www.plmb001.com/link/2ztHQRolCVeBL9un?mu=3

quantumultX v2ray订阅地址：
https://www.plmb001.com/link/2ztHQRolCVeBL9un?mu=4

clash托管地址：
https://www.plmb001.com/link/ZoGSjb2mkM3ovlWe

clashR托管地址：
https://www.plmb001.com/link/ZoGSjb2mkM3ovlWe?mu=1