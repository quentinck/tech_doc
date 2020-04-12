# 免费|申请GAE服务器[转载]

原文链接：https://zhuanlan.zhihu.com/p/60993816

免费试用申请链接地址：

```text
https://cloud.google.com/free/
```

## **前提准备**

已经注册了谷歌账号；

有visa等双币信用卡；

## **试用申请**

进入试用申请后，选择地区美国，目前中国好像还不支持；

![img](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/GAE申请/GAE申请v2-2ea770c340db155d9eb364d4b0127142_1440w.jpg)

填写个人信息：

账号类型需要选择个人，填写一个美国地区的地址即可，可以去[http://www.haoweichi.com/](https://link.zhihu.com/?target=http%3A//www.haoweichi.com/)获取：



![img](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/GAE申请/GAE申请v2-5abc819569960e2eb3af67daea7e41d7_1440w.jpg)





最后填写双币信用卡即可：



![img](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/GAE申请/GAE申请v2-be8f4123e391121ceb0d5e4fd4236869_1440w.jpg)



基本信息完成后，即可获得12个月的免费试用：



![img](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/GAE申请/GAE申请v2-3f61298d17c44bbfda9db5c9e9e9101d_1440w.jpg)





## **配置防火墙规则**

由于默认的防火墙规则限制太多，需要创建个新的防火墙规则：



![img](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/GAE申请/GAE申请v2-f8feba727ae3871a5dcf00c945f3e7b3_1440w.jpg)



具体配置如下图：



![img](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/GAE申请/GAE申请v2-5803a276fe1a46de5166ee3ff4af76e3_1440w.jpg)



建议将默认防火墙策略关闭，注意来源ip地址为”0.0.0.0/0”

## **申请长久的静态ip地址**

![img](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/GAE申请/GAE申请v2-d64389eee7bd77ff5819728d784c0323_1440w.jpg)

这里尽量选择亚洲区域，这样访问速度会快一些：



![img](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/GAE申请/GAE申请v2-d5cd03c17009fc243b34025f407d5bf4_1440w.jpg)



这里优先选择，asia-east1也就是台湾彰化地区的，因为该地区符合“优质的网络服务层级”，即google会将流量通过google的高品质全球主干网，在离用户最近的google边缘对接点进入和离开专有网络，也就是网速更快。



![img](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/GAE申请/GAE申请v2-c8a6792c66e176dcadb27806e244e151_1440w.jpg)



PS：静态ip只能申请一个

## **创建VM实例（vps）**

使用刚刚申请的静态ip，需要再在网络配置处选择静态的外部ip：



![img](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/GAE申请/GAE申请v2-e819f22672487868a0428b2e24426119_1440w.jpg)



如果想使用xshell等工具进行登录，可以在“安全”功能模块，配置ssh key，进行登录：

本地生成ssh key 命令：

```text
ssh-keygen -t rsa-f ./google -C root
```



![img](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/GAE申请/GAE申请v2-f41a626b068ce281d7c5eba2666369d7_1440w.jpg)



将生成的xxx.pub文件内容，拷贝到ssh密钥框中：



![img](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/GAE申请/GAE申请v2-89481e1732063b2b029543558f40d4f4_1440w.jpg)



创建成功后，可以使用ssh进行连接，google自带了可以在浏览器窗口打开的ssh：



![img](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/GAE申请/GAE申请v2-4321ad2ef784445b0a32ee56181ce0a4_1440w.jpg)



使用ssh key登录vps，需要修改下vi /etc/ssh/sshd_config的配置：

将允许root用户远程登录设置为yes;并允许使用publickey登录：

```text
PermitRootLogin yes
PubkeyAuthentication yes
```

当然也可以设置root密码，开启密码ssh登录,配置完成以后就可以搭建飞机场了。



## 补充说明

下述内容均为针对改文章的补充说明，个人信息详见附录

### 创建VM实例（vps）

1)  可先创建“实例模板”，后续如有错误，可删除服务器后，修改模板再次创建，默认使用Debian9系统；

2)  使用“实例模板”，需要单独设置：名称、服务器所在区域和外部IP，公钥；

3)  补充说明：创建VM实例后，进行网络设置，此部分说明不够详细；

4)  补充说明：这里使用Debian9版本作为服务器版本，网络使用台湾地区费用最低，使用最低配置；

个人ssh秘钥，详见附件

### SSH第三方客户端登陆

参考文章：https://www.vediotalk.com/archives/606步骤详细，且成功

 

1)  修改root账号密码(不要使用过于简单密码，容易产生安全性问题)

```
sudo passwd root
```

2)  切换到root账号

```
su root
```

3)  开启root账号下的ssh服务

CentOS和Debian通用，输入以下两条命令

```
sed -i 's/PermitRootLogin no/PermitRootLogin yes/g' /etc/ssh/sshd_config
sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
```

4)  重启ssh服务

```
/etc/init.d/ssh restart
```

5)  使用SSH客户端登陆

推荐使用xshell客户端；

 

备注：

1)  生成公共key方法：

ssh-keygen -t rsa -f ./google -C root

2)  使用浏览器进行SSH操作，可使用Ctrl+C/Ctrl+V进行命令拷贝

如需SSH客户端登陆操作，使用如下命令(参考文章中缺少一个空格)

3)  使用ssh下载文件方法：google.pub文件下载，可使用SSH浏览器方式登陆后，在屏幕右上方有下载选项；

 

### 使用google云搭建梯子

使用一键安装，并直接使用shadowsocks的客户端

 

输入下面命令回车

bash <(curl -s -L https://git.io/v2ray.sh)

shadowsocks配置信息：

1)  端口 30788(r2vay不能相同)

2)  密码

3)  加密方式 aes-256-cfb

 

安装完成后，可输入v2ray进行查询和管理

参考文档：

[https://github.com/233boy/v2ray/wiki/V2Ray%E6%90%AD%E5%BB%BA%E8%AF%A6%E7%BB%86%E5%9B%BE%E6%96%87%E6%95%99%E7%A8%8B](https://github.com/233boy/v2ray/wiki/V2Ray搭建详细图文教程)

###  google云服务链接：

https://console.cloud.google.com