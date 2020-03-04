# Nginx原理及使用

## Nginx原理说明

Nginx这里主要实现反向代理，即本地某个端口有代理服务，将其映射到外部客户端访问的某个端口上：端口映射和对应服务映射

基于nginx版本：1.10.3

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/04/20200304205536.png)



## Nginx配置

Nginx配置有两种方法：

### 方法一：使用工具进行配置(推测)

该方法应该是使用Linux配置文件的覆盖方法，具体原理尚未查询，该方法配置后，第二种方法失效

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

#### 方法二：配置Nignx文件

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