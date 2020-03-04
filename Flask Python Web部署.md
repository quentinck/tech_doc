# Flask Python Web部署

使用 Nginx + Gunicorn + Flask 将Web应用部署到服务器

## 原理说明

开发环境：Windows

部署环境：Linux/Debian、虚拟环境

开发工具：Pycharm

需要将Flask部署到服务器，你还需要两个东西：

1) Web服务器：Nginx、Apache 用于处理和响应HTTP请求

想要把Flask写的Web应用放到服务器上供他人访问，你不可能让用户使用Flask的5000端口来访问你的Web应用，所以你需要Nginx这个Web服务器做一个反向代理当用户访问你的域名时 nginx通过代理转到本地的5000端口

2)  WSGI容器：uWsgi、Gunicorn

Web框架（Flask）和Web服务器（Nginx）之间的通信，需要一套双方都遵守的接口协议。而WSGI协议就是用来统一这两者的接口的（WSGI是为Python语言定义的Web服务器和Web应用程序或框架之间的一种简单而通用的接口）。

Gunicorn和uWSGI是常用的WSGI容器，Gunicorn直接用命令启动，不需要编写配置文件，相对uWSGI要容易很多，所以这里我也选择用Gunicorn作为容器。（uWSGI让我更迷糊 Gunicorn简单点）

![基本原理](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/04/20200304195504.png)

-   Nginx：高性能 Web 服务器+负载均衡；

-   gunicorn：高性能 WSGI 服务器；

-   gevent：把 Python 同步代码变成异步协程的库；

-   Supervisor：监控服务进程的工具；

    部署参考链接：

    https://juejin.im/post/5de4d8135188255baf2f7587

    https://www.jianshu.com/p/d607ca5718a5

### Nginx



### gunicorn

如果让这个flask引用监听来自公网ip的请求，理论上你跑此程序的机器就相当于一个服务器了，然而这个服务器并不完美，所以我们需要nginx和gunicorn来增加它的功能，让它真刀真枪上生产环境的时候能按要求运行。

flask自带的WSGI框架性能很差劲，只能适用于开发环境调试使用。我们用专业一点的gunicorn(还有很多其他优秀的框架）替代flask自带的WSGI框架。

gunicorn也仅仅是一个python的WSGI框架而已，要让它真正处理来自互联网的各类访问功能还是有点欠缺，这时候就需要用到大名鼎鼎的nginx 服务器来替gunicorn遮风挡雨了

## 开发环境

开发环境：可使用pycharm专业版进行开发，开发环境部署参考pycharm说明文档

部署环境：

### Nginx

#### 安装

目标：使用nginx进行本地程序/网页的反向代理配置，外网可以访问内网程序

sudo apt-get install nginx

使用虚拟环境后，安装路径如下：

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/04/20200304201011.png)

默认应该是80端口，浏览器可输入IP地址进行测试，例如：

http://34.80.6.92/

可通过下述命令测试网页的有效性

```
sudo service nginx stop
sudo service nginx restart
```

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/04/20200304201036.png)

**注意：**

1.  nginx安装后就会默认启动，但如果发生端口冲突，则会启动失败
2.  默认80端口在/etc/nginx/sites-available/default文件中定义，需要删除80端口默认链接，避免冲突：rm /etc/nginx/sites-enabled/default
3.  编辑/etc/nginx/nginx.conf 文件，把 server_tokens off 前的注释删除，防止暴露 nginx 和服务器的版本号
4.  可通过netstat -ntpl命令查看端口使用情况；

#### 反向代理配置

l nginx默认配置路径为：/etc/nginx/nginx.conf，调用/etc/nginx/sites-enabled/中的文件

l /etc/nginx/sites-enabled/*中的文件为/etc/nginx/sites-available文件进行链接，sites-enabled中所有文件为快捷方式

基本原理说明详见附录(ck实测)

1)  自行添加配置信息

新建/etc/nginx/sites-available/flask文件，将下述配置拷贝到该文件中

```
vi /etc/nginx/sites-available/flask
```

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

然后建立链接：

```
sudo ln -s /etc/nginx/sites-available/flask /etc/nginx/sites-enabled 
```

使能该功能：

```
sudo service nginx stop
sudo service nginx restart
```

此时访问http://ip:5000端口，显示如下：

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/04/20200304201412.png)           

至此，已经开启Nginx默认代理，下一步与flask_hello.py链接起来

注意：

1.  python hello.py和nginx使用同一个端口，nginx运行后会与hello.py冲突；
2.  经过测试，nginx默认会在reboot后自动启动，如需测试，需要停止该服务，可以使用Kill命令关闭冲突的进程，参考附录的命令；

### gunicorn

参考：https://www.jianshu.com/p/69e75fc3e08e

目标：使用gunicor启动http服务

#### 安装

```
pip3 install gunicorn
```

查看命令行选项： 安装gunicorn成功后，通过命令行的方式可以查看gunicorn的使用信息。

```
gunicorn -h
```

如果安装时未使用虚拟环境，需要建立程序链接：

```
ln /usr/local/python3.7.6/bin/gunicorn /usr/bin/gunicorn
```

#### 测试

测试程序：

```
cd /home/web
```

测试命令1：

```
gunicorn flask_hello:app
```

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/04/20200304201714.png)

测试命令2：

```
gunicorn -w 4 -b 127.0.0.1:5000 flask_hello:app
```

按下按键ctrl+z退出当前线程，可通过ps查看线程运行情况，此时如果使用nginx进行代理配置监控5000端口，同时映射到81外网端口，可在外网访问该程序；

#### 使用文件配置

使用配置文件启动程序

```
gunicorn flask_hello:app -c hello_gunicorn.py
```

查看状态

```
pstree -ap|grep gunicorn
```

```
vi /home/web/hello_gunicorn.py
```

编写配置程序

```
import multiprocessing
bind = '127.0.0.1:5000'
```

备注：

问题1：RuntimeError: gevent worker requires gevent 1.4 or higher

```
pip install gevent
```

##### 详细配置文件hello_gunicorn.py

```
#!/home/xx/.virtualenvs/xx/bin/python
# encoding: utf-8
import multiprocessing
# 监听端口
bind = '127.0.0.1:5000'
# 工作模式
worker_class = 'gevent'
# 并行工作进程数
workers = multiprocessing.cpu_count() * 1
# 设置守护进程
daemon = True
# 设置日志记录水平
loglevel = 'debug'
# 设置错误信息日志路径
errorlog = './log/error.log'
# 设置访问日志路径
accesslog = './log/access.log'
```

### Supervisor(python3)

#### Supervisor 介绍

参考文档：https://www.jianshu.com/p/ba6327f198ce
Supervisor是用Python开发的一套通用的进程管理程序，能将一个普通的命令行进程变为后台daemon，并监控进程状态，异常退出时能自动重启。它是通过fork/exec的方式把这些被管理的进程当作supervisor的子进程来启动，这样只要在supervisor的配置文件中，把要管理的进程的可执行文件的路径写进去即可。也实现当子进程挂掉的时候，父进程可以准确获取子进程挂掉的信息的，可以选择是否自己启动和报警。
官网：http://supervisord.org/installing.html
默认配置说明
默认的配置文件是下面这样的，但是这里有个坑需要注意，supervisord.pid 以及 supervisor.sock 是放在 /tmp 目录下，但是 /tmp 目录是存放临时文件，里面的文件是会被 Linux 系统删除的，一旦这些文件丢失，就无法再通过 supervisorctl 来执行 restart 和 stop 命令了，将只会得到 unix:///tmp/supervisor.sock 不存在的错误 。

参考文档：https://www.jianshu.com/p/bf2b3f4dec73

官网：[http://supervisord.org/installing.html](https://links.jianshu.com/go?to=http%3A%2F%2Fsupervisord.org%2Finstalling.html)



终于在Python3下可以正常使用pip安装了。

```
pip3 install supervisor
```

supervisor安装完成后，会生成三个执行程序：supervisord、supervisorctl、echo_supervisord_conf，分别是supervisor的守护进程服务（用于接收进程管理命令）、客户端（用于和守护进程通信，发送管理进程的指令）、生成初始配置文件程序。

#### 手动进行管理

```
supervisorctl
```

#### 使用配置文件管理

注意：手动创建和加载配置文件

```
cd /home/web
mkdir Supervisor
cd Supervisor/
echo_supervisord_conf > supervisor.conf
cat supervisor.conf 
```

修改1：修改supervisor.conf

这里把所有的/tmp路径改掉，详见备注说明；

修改2：添加个人工程的配置信息flask_hello.ini

进程管理配置参数，不建议全都写在supervisor.conf 文件中，建议每个进程写一个配置文件，并放在include配置块中files指定的目录下，通过include包含进 supervisor.conf 文件中。

```
vim /home/web/Supervisor/flask_hello.ini
```

```
;flask_hello.ini内容
[program:flask_hello]
directory=/home/web/                             ; 项目地址
command= gunicorn flask_hello:app -c hello_gunicorn.py ; 启动命令
autostart=true                                    ; 在 supervisord 启动的时候也自动启动，如果设置为false 重启服务器后还需要手动执行命令进行运行
autorestart=true                                         ; 程序异常退出后自动重启 设置为false supervisord 将不会在程序关闭后重新运行、设置
stderr_logfile=/home/web/flask_hello.err.log              ; 错误日志
stdout_logfile=/home/web/flask_hello.out.log              ; 所有日志
```

注：supervisor不会自动创建文件，所以日志文件要提前建好

修改/home/web/Supervisor/supervisor.conf配置文件

注意：supervisord.conf文件是使用echo_supervisord_conf工具自建

修改3：将flask_hello.ini配置写入supervisor.conf文件中

```
vim /home/web/Supervisor/supervisor.conf
# 最后加上
[include]
;files = relative/directory/*.ini
files = /home/web/Supervisor/*.ini
```

启动服务：

```
supervisord -c /home/web/Supervisor/supervisord.conf
```

或者

```
sudo service supervisor restart
```

查看supervisor是否启动成功

```
ps -ef|grep supervisord
```

至此，可使用81端口访问flask_hello.py程序

重启服务：

1)   查看线程：ps -ef|grep supervisord

2)   Kill掉该线程：kill -s 987

3)   再次启动线程：supervisord -c /home/web/Supervisor/supervisord.conf

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/04/20200304202642.png)

备注：

##### 问题1：unix:///tmp/supervisor.sock no such file

该错误说明supervisord.conf中有错误，可将部分无效内容屏蔽，这里需要注意，supervisord.conf任务错误都会导致配置文件导入失败；

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/04/20200304202558.png)

解决办法：

第一步：

这里把所有的/tmp路径改掉，例如：/tmp/supervisor.sock 改成 /var/run/supervisor.sock

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/04/20200304202709.png)

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/04/20200304202717.png)



其他启用的部分不赘述；

修改supervisor.conf 配置文件，修改如下标示的几行即可：

```
[unix_http_server]
;file=/tmp/supervisor.sock   ; (the path to the socket file)
file=/var/run/supervisor.sock   ; 修改为 /var/run 目录，避免被系统删除
 
[supervisord]
;logfile=/tmp/supervisord.log ; (main log file;default $CWD/supervisord.log)
logfile=/var/log/supervisor/supervisord.log ; 修改为 /var/log 目录，避免被系统删除
pidfile=/var/run/supervisord.pid ; 修改为 /var/run 目录，避免被系统删除
 
[supervisorctl]
; 必须和'unix_http_server'里面的设定匹配
;serverurl=unix:///tmp/supervisor.sock ; use a unix:// URL  for a unix socket
serverurl=unix:///var/run/supervisor.sock ; 修改为 /var/run 目录，避免被系统删除
```

 

第二步：unix:///var/run/supervisor.sock no such file

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/04/20200304202759.png)

```
udo touch /var/run/supervisor.sock
sudo chmod 777 /var/run/supervisor.sock
sudo service supervisor restart
```

第三步：supervisorctl unix:///var/run/supervisor.sock refused connection

```
unlink /var/run/supervisor.sock
unlink /tmp/supervisor.sock
```

##### 问题2：Failed to restart supervisord.service: Unit supervisord.service not found.

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/04/20200304202829.png)

解决办法：要是用 supervisord -c /etc/supervisor.conf 来启动进程，就不要用 services 来重启。 建议你 kill 掉 supervisord，再直接用 services 来启动 supervisord。

#### 配置说明

配置详解：
a)  在supervisord.conf文件中，分号“；”后面的内容表示注释
b)  [group:组名]，设置一个服务分组，programs后面跟组内所有服务的名字，以分号分格。
c)  [program：服务名]，下面是这个服务的具体设置：
Command:启用Tornado服务文件的命令，也就是我们手动启动的命令。
Directory:服务文件所在的目录
User:启用服务的用户
Autorestart:是否自动重启服务
stdout_logfile：服务的产生的日起文件
loglevel:日志级别

 

#### 其他命令

1)  指定端口运行

如果更改了/etc/supervisord.conf中的端口号，原来的简写命令

```
# supervisorctl
```

就需要在后面指定supervsor配置文件位置，或指定supervisor服务运行的端口号

```
supervisorctl -c /etc/supervisord.conf 
supervisorctl -s http://localhost:7001
```

 否则会报连接拒绝

```
# supervisorctl 
```

http://localhost:9001 refused connection

supervisor> 

 2)  重启服务

```
supervisorctl shutdown
supervisorctl -c /home/web/Supervisor/supervisord.conf
```

 

如果一切正常，做完这所有步骤之后，现在公网的ip访问你的主机，就可以打开你的flask应用了

然后去浏览器输入命令： 公网ip:81 回车就能看到效果

 

## 生成项目依赖软件列表

为了方便在服务器上一次性安装，我们将全部依赖写入一个叫 requirements.txt 的文本文件中。激活本地的虚拟环境（如果你使用了虚拟环境的话），并进入项目的根目录，运行 pip freeze > requirements.txt 命令：

(blogproject_env) C:\Users\yangxg\Workspace\blogproject>

pip freeze > requirements.txt

flask_hello环境里面的依赖关系如下：

```
Click==7.0
Flask==1.1.1
gevent==1.4.0
greenlet==0.4.15
gunicorn==20.0.4
itsdangerous==1.1.0
Jinja2==2.11.1
MarkupSafe==1.1.1
supervisor==4.1.0
Werkzeug==1.0.0
```

这时项目根目录下会生成了一个 requirements.txt 的文本文件，其内容记录了项目的全部依赖。

可在虚拟环境下一次安装所以依赖

先安装python3.7.6

```
workon flask_hello
pip install -r requirements.txt
```

## 使用docker打包项目

https://zhuanlan.zhihu.com/p/78432719

## 附录

### 设置完成后的启动命令汇总(linux)

| 目的                                                         | 命令                                                         | 命令说明                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 使用flask+nginx+gunicorn将内部5000端口的程序，映射到外网81端口 | workon  flask_env  sudo  service nginx restart  gunicorn -w  4 -b 127.0.0.1:5000 flask_hello:app | 启动虚拟环境  启动nginx反向代理  启动flask_hello程序，使用5000端口 |
| 使用gunicorn配置                                             | workon  flask_env  sudo  service nginx restart  gunicorn -w  4 -b 127.0.0.1:5000  flask_hello:app  或者  gunicorn flask_hello:app -c hello_gunicorn.py |                                                              |
| 使用supervisor管理进程                                       | workon  flask_env    `supervisord -c /home/web/Supervisor/supervisor.conf` | nginx会自动运行                                              |

 

### 手动环境部署

### 安装Flask

首先进入flask虚拟环境，安装flask1.1.1(与pycharm版本一致)

```
pip3 install flask==1.1.1
```

查看当前解释器安装的第三方包

```
pip freeze
```

查看虚拟环境所在路径

```
which python
```

### 运行测试程序

编写Flask的helloworld代码

目标：在本地能够运行127.0.0.1:5000运行helloword代码

```
# 开始我们的第一个flask程序from flask import Flask
# 1.创建web应用

app = Flask(__name__)

# 2.定义路由
@app.route('/')
def index():
    return "<h1 style='color:red'>Hello World</h1>"

 # 3.运行web应用
if __name__ == '__main__':
app.run()
```



 运行情况如下：

(flask_env) root@quentin:/home/web# python flask_hello.py

 \* Serving Flask app "flask_hello" (lazy loading)

 \* Environment: production

  WARNING: This is a development server. Do not use it in a production deployment.

  Use a production WSGI server instead.

 \* Debug mode: off

 \* Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)