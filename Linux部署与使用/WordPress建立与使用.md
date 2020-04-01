# WordPress建立与使用

## WordPress使用

### WordPress的IP隐藏

设置->WordPress地址(URL)，修改为：http://www.xtep2020.club

站点地址(URL)，修改为：http://www.xtep2020.club

上述地址需要与nginx的反向链接地址一致，可使用自定义的端口号；

### 优酷视频链接

```
<iframe height="498" width="510" src="http://player.youku.com/embed/XMTMyOTczNjY2MA==" frameborder="0" 'allowfullscreen'=""></iframe>
```

其中**XMTMyOTczNjY2MA**为视频的ID，替换即可；

### 插件

插件推荐：https://zhuanlan.zhihu.com/p/34314017



## WordPress建立

WordPress建立共有三种方式：

1.  使用GAE自建服务器搭建；
2.  使用GAE的Docker(可使用Portainer模块)；
3.  使用Google的应用建立；



### 使用Docker搭建

首选该方式，该服务器剩余性能可做其他用途，目前该方式对于性能要求较低的应用可同时运行多个容器应用。

该方式前置条件：已安装Portainer，并加入WordPress(会自动加入MySql容器)和Nginx容器；

#### Portainer配置wordpress

每一个Docker容器内本身就是一个极其精简的Linux系统，并且多数都是基于Debian/Ubuntu的。这个Nginx的容器也是如此，我们现在进入到这个容器内要做的就是配置Nginx实现反向代理WordPress。因为它太精简，所以我们需要先安装一些常用的编辑工具：

**进行WordPress的端口配置和Nginx端口配置，然后进行映射**

参考文档：http://www.xuxiaobo.com/?p=5481

文档中nginx配置有错误，下述部分经过验证：

```
apt -y update && apt -y install nano
nano /etc/nginx/conf.d/wordpress.conf
```

```
server {    
   listen    80;     
   server_name www.xtep2020.club;
   location / {     
      proxy_pass    http://34.80.6.92:32772;     
      proxy_redirect       off;     
      proxy_http_version     1.1;     
      proxy_set_header Upgrade  $http_upgrade;     
      proxy_set_header Connection "upgrade";     
      proxy_set_header Host   $host;     
      proxy_set_header X-Real-IP $remote_addr;     
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;     
   }   
}
```

```
/etc/init.d/nginx restart
```

### GAE应用

如作为个人长期博客可使用，费用为$13.61/月，无需进行环境搭建

使用APP Engine搭建：https://console.cloud.google.com/marketplace/details/click-to-deploy-images/wordpress?pli=1&_ga=2.20105208.1589394462.1582460562-619017045.1581314921

可在marketplace里面自由搜索



### GAE服务器自建(不建议)

**该方式耗时较长，不建议使用**

使用Linux VPS 一键安装 LNMP：

```
wget https://vps234.oss-cn-shanghai.aliyuncs.com/download/lnmp.tar.gz -cO lnmp1.5.tar.gz && tar zxf lnmp1.5.tar.gz && cd lnmp && ./install.sh lnmp
```

解压WordPress包

```
tar -zxvf wordpress-4.7.2-zh_CN.tar.gz
```

进入根目录上一级目录

```
chown -R 755 /home/www/wordpress
chown -R www:www /home/www/wordpress
```

参考文档：

https://www.vps234.com/linux-vps-install-wordpress-tutorials-by-lnmp/#wordpress-lnmp-block3

