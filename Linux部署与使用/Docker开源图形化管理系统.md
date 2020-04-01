# Docker使用

安装前的说明：

Docker是容器工具，Portainer是UI管理界面工具

### Docker中容器和镜像的关系

docker中容器和镜像的关系是什么？
最近学习了docker，感觉容器和镜像学的有点模糊。

特别是镜像和容器，感觉完全分不开，所以在此学习，然后总结了一下，便于后面的学习。

 

docker的整个生命周期有三部分组成：镜像（image）+容器（container）+仓库（repository）。

    docker 容器=镜像+可读层
容器是由镜像实例化而来。

简单来说，镜像是文件，容器是进程。

容器是基于镜像创建的，即容器中的进程依赖于镜像中的文件。

可通过以下语句实现仓库中的镜像查询：

```
docker search aliddns
```

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/31/20200331141725.png)

参考：https://www.cnblogs.com/wushuaishuai/p/9984228.html


## Docker在Win10下的安装和配置

### 第一步：安装Docker

下载Docker For Windows安装包：[下载地址](https://store.docker.com/editions/community/docker-ce-desktop-windows)

运行安装包，全自动安装完成。

### 第二步：安装Portainer

打开命令行工具，执行

```
docker pull portainer/portainer
```

拉取portainer镜像。

```
docker volume create portainer_data
```

检查镜像是否存在:

```
docker images
```



启动portainer命令

```
docker run -d -p 9000:9000 --restart=always --name portainer -v /var/run/docker.sock:/var/run/docker.sock -v /Users/name/dev/docker_file/portainer/data:/data docker.io/portainer/portainer
```

备选：

```
docker run -d -p 9000:9000 --restart=always --name portainer -v /var/run/docker.sock:/var/run/docker.sock -v /d/Docker/Container_Data/portainer:/data portainer/portainer
```

tips：在运行docker容器时可以加如下参数来保证每次docker服务重启后容器也自动重启：`--restart=always`

如果已经启动了则可以使用如下命令：

```
docker update --restart=always portainer
```

在浏览器输入[http://localhost:9000](https://links.jianshu.com/go?to=http%3A%2F%2Flocalhost%3A9000%2F)访问portainer管理后台，设置admin的登录密码。



## 配置Portainer

### 使用本地配置

即，配置项选第一项，图片略

### 远程配置如下(暂未使用，成功过一次)

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/17/20200317163421.png)

docker.for.win.localhost:2375

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/17/20200317163539.png)



## 部署Linux的Docker环境

本章节目的在于制作一个包含Docker的Linux环境，用于Docker镜像的打包

windows下已经安装Docker，可打开cmd运行命令行

docker操作参考文档：[Win10中docker的安装与使用](https://blog.csdn.net/zzq060143/article/details/91050272)

常见使用方法：https://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html

#### 安装ubuntu镜像(ubuntu无效)

查看docker状态：

```
docker version
docer ps
docker info
```

拉取ubuntu镜像

```
docker run -it debian bash
```

大概是几十兆吧，所以直接启用了，输入exit命令停止容器

安装完成后自动进入该Linux环境，此时再输入docker命令是无效的

Docker安装环境

参考：https://docs.docker.com/install/linux/docker-ce/debian/

对应的中文说明：https://www.runoob.com/docker/debian-docker-install.html

更新环境

```
apt-get update
```

更新依赖

```
apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common
```

```
curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
```

```
apt-key fingerprint 0EBFCD88
```

```
add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
  $(lsb_release -cs) \
  stable"
```

```
apt-get update
```

安装最新版本的 Docker Engine-Community 和 containerd 

```
apt-get install docker-ce docker-ce-cli containerd.io
```

或者

```
apt-get install -y docker.io
```

重启debian镜像服务，使用Portainer重启Restart

安装完成后可能需要启动下

```
service docker start
```

查看docker是否安装成功

```
docker --version
```

测试

```
docker run hello-world
```

### docker-compose安装



### 配置flask_jsondash容器





### dockerize 

https://github.com/jwilder/dockerize

```
apt-get update && apt-get install -y wget
```

可自行设置dockerize版本，这里目前是v0.6.1

```
DOCKERIZE_VERSION=v0.6.1
wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz
```



### 拉取python3.7环境(可选)

```
docker pull python:3.7
docker ps
```

手动拉取的镜像可以在Images里面找到并启用



### flask_jsondash

#### 安装git&gcc

```
apt install git
```

```
apt-get install make gcc
```

```
docker version
```

```
git clone https://github.com/christabor/flask_jsondash.git
cd flask_jsondash/
make dockerize
```

