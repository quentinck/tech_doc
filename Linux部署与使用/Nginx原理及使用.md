# Nginx原理及使用

## Nginx原理说明

Nginx这里主要实现反向代理，即本地某个端口有代理服务，将其映射到外部客户端访问的某个端口上：端口映射和对应服务映射

基于nginx版本：1.10.3

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/04/20200304205536.png)



## Nginx在Docker下的配置原理及操作说明

使用Docker添加Nginx后，默认的服务器为(端口可能不同)：http://10.0.0.14:32775/，此时可通过此地址访问Nginx服务界面

对于Nginx服务的配置，分为两部分：

1.  Portainer服务所在服务器的端口映射到container对应的端口；

2.  Nginx对于对应端口的监听及链接；

    如下所示：

    1.在portainer中配置，将服务器的81~83端口由nginx接管，映射到Nginx的容器中：

    ![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/31/20200331113817.png)

2.  在Nginx容器中进行端口监听及映射

    ![image-20200331114010246](C:/Users/quent/AppData/Roaming/Typora/typora-user-images/image-20200331114010246.png)

3.  路由器端口转发：

    转发到nginx代理服务器的IP

    ![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/31/20200331125701.png)

**配置内网Nginx代理，实现IP+端口转移**

可实现：http://10.0.0.14:83/访问转移到http://10.0.0.15:81/，即IP及端口转移

```
apt -y update && apt -y install nano
nano /etc/nginx/conf.d/wiki.conf
```

```
server {    
   listen    83;     
   server_name http://10.0.0.14:83/;
   
   location / {     
      proxy_pass    http://10.0.0.15:81/;         
   }   
}
```

```
/etc/init.d/nginx restart
```

**配置外网，实现域名+端口转移**

可实现：http://wiki.quentinck.cn:81/访问转移到http://10.0.0.15:81/，即域名转移

```
server {    
   listen    83;     
   server_name http://wiki.igpsport.top:83/;
   
   location / {     
      proxy_pass    http://10.0.0.15:81/;         
   }   
}
```

**配置外网80端口转移**

修改/etc/nginx/conf.d/default.conf，去掉默认的80端口配置

```
mv /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.confbak
/etc/init.d/nginx restart
```



## Nginx配置流程说明

配置文件基本流程(ck推理)

1.  nginx一般配置文件在/etc/nginx目录下
2.  先读取/etc/nginx/nginx.conf文件
3.  该文件在http服务中读取/etc/nginx/conf.d中的内容：

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/04/20200304205742.png)

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/04/20200304205749.png)

其中有log日志及相关配置文件

1)  sites-enabled 和sites-available文件夹的关系

将需要的配置放到sites-available中存储，需要启用的使用ln进行连接到sites-enabled，可参考site-enable/default文档最后的说明

测试：直接修改配置有效的测试办法：

```
vi /etc/nginx/sites-enabled/default
```

自行添加端口号为81的服务：

```
server {
    listen 81;                 #监听81端口
    server_name 34.80.6.92     #监听的host
    charset utf-8;
    
    location / {  
    proxy_pass http://127.0.0.1:5000; # 代理本机127.0.0.1:5000的服务  
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

2)  自行添加配置信息

新建/etc/nginx/sites-available/flask文件，将上述配置拷贝到该文件中

然后建立链接：

```
sudo ln -s /etc/nginx/sites-available/flask /etc/nginx/sites-enabled 
```

使能该功能：

```
sudo service nginx stop
sudo service nginx restart
```

nginx参数修改可参考，该文档主要描述了nginx的配置文档依赖关系：

https://www.jianshu.com/p/aed6b5204225

下述文档描述nginx的代理原理：

https://zhuanlan.zhihu.com/p/56011629

### Nginx的WordPress配置

配置内容如下:

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

#### 

## Nginx基本操作

启动： nginx

停止/重启： nginx -s stop(quit、reload)

帮助： nginx -h

配置文件： vim /usr/local/nginx/conf/nginx.conf

查询路径：which nginx

```
sudo service nginx reload
sudo service nginx restart
```