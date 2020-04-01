# DokuWiki建立与使用

## 安装dokuwiki

创建虚拟环境：

```
mkvirtualenv -p python3 dokuwiki_env
```

进入该虚拟环境：

```
Workon dokuwiki_env
```

dokuwiki安装参考：

https://blog.csdn.net/ljskr/article/details/84563894

更新系统

```
apt update && apt upgrade -y
```

 

### 下载 dokuwiki 源码

进入官网( https://www.dokuwiki.org/dokuwiki )下载 dokuwiki 源码，

解压到 /var/www/dokuwiki 路径下，并使用以下命令更改 dokuwiki 的目录权限

```
cd /home/www
wget https://download.dokuwiki.org/src/dokuwiki/dokuwiki-stable.tgz 
tar -xzvf dokuwiki-stable.tgz
```

修改文件夹名称及权限

```
mv dokuwiki-2018-04-22b dokuwiki
sudo chown -R www-data:www-data /home/www/dokuwiki
```

修改后：使用github上的版本：

https://github.com/splitbrain/dokuwiki

### 增加 nginx 配置

在 /etc/nginx/sites-available 目录下增加一个文件名叫 dokuwiki

sudo vi /etc/nginx/sites-available/dokuwiki

```
server {
    listen [::]:81;
    listen 81;
 
    server_name wiki.example.com; # Replace with your hostname
    root /home/www/dokuwiki;
    index index.html index.htm index.php doku.php;
 
    client_max_body_size 15M;
    client_body_buffer_size 128K;
 
    location / {
        try_files $uri $uri/ @dokuwiki;
    }
 
    location ^~ /conf/ { return 403; }
    location ^~ /data/ { return 403; }
    location ~ /\.ht { deny all; }
 
    location @dokuwiki {
        rewrite ^/_media/(.*) /lib/exe/fetch.php?media=$1 last;
        rewrite ^/_detail/(.*) /lib/exe/detail.php?media=$1 last;
        rewrite ^/_export/([^/]+)/(.*) /doku.php?do=export_$1&id=$2 last;
        rewrite ^/(.*) /doku.php?id=$1 last;
    }
    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
        fastcgi_index  index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}
```

启用该站点配置，在sites-enabled目录下创建一个软链接：

```
sudo ln -s /etc/nginx/sites-available/dokuwiki /etc/nginx/sites-enabled/
```

启动 nginx

运行命令

```
sudo service nginx restart
```

访问地址：

http://34.80.6.92:81

 

### 安装dokuwiki

打开浏览器，输入http://34.80.6.92:81/install.php， 按照页面提示步骤进行安装。

 

### 插件安装

https://www.jianshu.com/p/d986ec44d5f3

1)Markdown插件Markdown Page Plugin

2)  [**imgpaste**](https://link.jianshu.com/?t=https://www.dokuwiki.org/plugin:imgpaste)：在编辑器直接粘贴就可以插入剪贴板中的图片，可以用来快速上传截图。

3)  [**Note**](https://link.jianshu.com/?t=https://www.dokuwiki.org/plugin:note)：可以在页面中插入醒目的提示文字，有几种默认图标和样式。

4)  中文文件名乱码

修改dokuwiki/conf/local.php在最后一行加上：

$conf['fnencode'] = 'utf-8';

3）editor.md

```
wget https://github.com/pandao/editor.md/archive/v1.5.0.tar.gz
tar -xzvf v1.5.0.tar.gz
mv editor.md-1.5.0 /home/www/dokuwiki/lib/editor.md
```

