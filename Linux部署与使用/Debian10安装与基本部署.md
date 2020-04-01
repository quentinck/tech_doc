## 安装工具说明

使用rufus-3.9p烧录镜像到U盘进行安装，选择UEFI模式；

选择文件之后
软件会**自动识别你要烧录的文件的类型，弹出提示，从网络上下载必要的引导文件**

镜像下载地址：

https://developer.aliyun.com/mirror/



## 安装说明

#### 基本安装

https://blog.csdn.net/Aria_Miazzy/article/details/84704388

1.  选择“Graphical Installer”进行安装，不是选择第一项；
2.  语言选择的英文(默认值)；
3.  主机名称“Hostname”：qwkj-debian
4.  域名"Domain name"：空
5.  root password:qwkj
6.  选择第三项：Guided - use entre disk and set up LVM)
7.  推荐使用第三列（Separate /home , /var , and /tmp partitions）
8.  安装Grub。这个服务器只有一个硬盘，所以我在这里选择/ dev / sda。

#### 配置SSH服务

1.  配置网络

    默认情况下，ifconfig等网络工具不可用。安装包：

    ```
    sudo apt-get install net-tools
    ```

2.  安装SSH服务

    ```
    $ sudo apt-get install openssh-server
    ```

    接下来，立即启动**sshd**服务，然后使用[systemctl命令](https://www.howtoing.com/manage-services-using-systemd-and-systemctl-in-linux/)检查它是否已启动并运行，如下所示。

    ```
    $ sudo systemctl start sshd
    $ sudo systemctl status sshd
    ```

11.  开启SSH服务

修改/etc/ssh/sshd_config

```
vi  /etc/ssh/sshd_config
```

```
PasswordAuthentication yes
PermitRootLogin yes
```

重启服务

```
service ssh restart
```

添加开机自启动 (默认自启动，可不添加)

```
update-rc.d ssh enable
```



12.  IP修改

路由器中设置74:27:EA:5F:F6:54的IP为14，本机就不做修改；

如果本地修改，静态Ip设置和子网掩码设置的命令后面不能跟注释

下述修改暂不成功：

```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
#allow-hotplug enp2s0
#iface enp2s0 inet dhcp

# The primary network interface
auto enp2s0 
iface enp2s0 inet static
        address 10.0.0.14
        netmask 255.255.255.0
        gateway 10.0.0.1
```

### 系统常用服务安装

更新系统

```
apt update && apt upgrade -y
apt-get update
apt-get upgrade
```

等待进度走完之后,依次安装,保证环境正常:

```
apt-get install -y make build-essential gcc libffi-dev libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev
```

4)  安装gcc

```
sudo apt-get install make gcc
```

5)  安装zlib

```
wget http://www.zlib.net/zlib-1.2.11.tar.gz
tar xzvf zlib-1.2.11.tar.gz
cd zlib-1.2.11
./configure
make
make install
```



## 安装Docker

```shell
curl -sSL https://get.docker.com/ | sh
```

开启docker服务并设置开机启动

```
systemctl start docker.service  
systemctl enable docker.service
```

### Portainer面板安装

https://www.vpslala.com/t/179

然后创建Portainer卷

```shell
docker volume create portainer_data
```

安装docker面板Portainer

```shell
docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
```

访问：你的ip:9000

Portainer使用local模式建立wordpress，参考：https://www.sohu.com/a/317494597_100299155



#### Nginx服务器设置

### 使用Docker搭建

首选该方式，该服务器剩余性能可做其他用途，目前该方式对于性能要求较低的应用可同时运行多个容器应用。

该方式前置条件：已安装Portainer，并加入WordPress(会自动加入MySql容器)和Nginx容器；

#### Portainer配置禅道

每一个Docker容器内本身就是一个极其精简的Linux系统，并且多数都是基于Debian/Ubuntu的。这个Nginx的容器也是如此，我们现在进入到这个容器内要做的就是配置Nginx实现反向代理WordPress。因为它太精简，所以我们需要先安装一些常用的编辑工具：

**进行禅道的端口配置和Nginx端口配置，然后进行映射**

**下述操作都是在Nginx的Docker中进行配置，可在Portainer的界面进行操作。**

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/31/20200331090331.png)

参考文档：http://www.xuxiaobo.com/?p=5481

文档中nginx配置有错误，下述部分经过验证，通过ctrl+o保存，ctrl+x退出



#### 测试wiki代理：

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

### http://10.0.0.14:32771/

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
