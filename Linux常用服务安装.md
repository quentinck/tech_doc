# Linux常用服务安装

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

### Portainer使用remote（未使用，验证有问题）

https://blog.csdn.net/Viogs/article/details/93742373

远程remote端口开启，可参考官方文档中的命令：

https://docs.docker.com/install/linux/linux-postinstall/



注意：开启remote后，部分命令失效，例如：docker pull portainer/portainer

和docker volume create portainer_data 

```
sudo systemctl edit docker.service
```

```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H fd:// -H tcp://127.0.0.1:2375         
```

```
sudo systemctl daemon-reload
sudo systemctl restart docker.service
```

查询配置情况：

```
sudo netstat -lntp | grep dockerd
```

上述修改的文档为：vi /etc/systemd/system/docker.service.d/override.conf

删除该文档，可使得该配置无效。

 

也可手动修改(验证未能成功，与方法一冲突，主要是文件overwrite导致)

需开启remote端口2375

```
vim /lib/systemd/system/docker.service
ExecStart=/usr/bin/dockerd -H tcp://127.0.0.1:2375
```

重启客户机docker

```
systemctl daemon-reload 
systemctl restart docker
```

测试端口(单个命令运行)： 

```
docker -H localhost:2375 version
curl -v -X GET localhost:2375/_ping
systemctl show --property=FragmentPath docker
```

参考：https://blog.csdn.net/ZYC88888/article/details/90231871

也可参考官方文档：https://docs.docker.com/install/linux/linux-postinstall/

查看docker端口情况：

```
netstat -lntp | grep dockerd
```

查看进程：

```
ps aux | grep dockerd
```

使用参考：

https://blog.51cto.com/bovin/2170723

方法二：

参考文档：https://cloud.tencent.com/developer/article/1360720

```shell
sudo apt update
sudo apt install apt-transport-https ca-certificates curl gnupg2 software-properties-common
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
sudo apt update
apt-cache policy docker-ce
sudo apt install docker-ce
sudo systemctl status docker
```

测试：要检查您是否可以从Docker Hub访问和下载图像，请键入：

```shell
docker run hello-world
```

### Portainer配置wordpress

每一个Docker容器内本身就是一个极其精简的Linux系统，并且多数都是基于Debian/Ubuntu的。这个Nginx的容器也是如此，我们现在进入到这个容器内要做的就是配置Nginx实现反向代理WordPress。因为它太精简，所以我们需要先安装一些常用的编辑工具：

http://www.xuxiaobo.com/?p=5481

文档中错误：

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

备注1:

第一次生成wordpress后，其容器内的端口已经确定，推测如果需要改动，需要在wordpress容器内通过命令行改动

## 安装python3.7.6

### 环境准备

新apt源,如果速度慢,可以修改apt源(/etc/apt/sources.list),依次输入:

```shell
apt-get update
apt-get upgrade
```

等待进度走完之后,依次安装,保证环境正常：

```shell
apt-get install -y make build-essential gcc libffi-dev libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev 
```

### 下载python3.7.6

查询最新的python版本：https://www.python.org/downloads/

找到下载链接：[https://www.python.org/ftp/python/3.7.6/Python-3.7.6.tgz](https://www.python.org/ftp/python/3.8.1/Python-3.8.1.tgz)

考虑到部分软件不支持新版本的python，比如tensorflow支持3.5~3.7，故需要考虑python版本问题

创建目录python3.7.6安装目录(黄色部分自行修改连接)，统一放到~/tools目录下

```shell
wget https://www.python.org/ftp/python/3.7.6/Python-3.7.6.tgz
```

解压：

```shell
tar -xzvf Python-3.7.6.tgz
```

这里需要注意，python-3.7.6目录在/usr/local下，如果有多层目录，make install时候会存在python3.7文件不再/usr/bin目录所以无法调用的情况(未验证)

### 安装python3.7.6

默认安装路径为：/usr/local/python3.7.6

```shell
cd Python-3.7.6
./configure -prefix=/usr/local/python3.7.6 --with-ssl
make
make install
```

备注1：

安装出错，需要按照必要的编译环境：

configure: error: in `/root/Python-3.7.6':

configure: error: no acceptable C compiler found in $PATH

See `config.log' for more details

备注2：

如果出现以下错误，缺少zlib包原因，安装zlib后

重新执行make && make install安装python：

zipimport.ZipImportError: can't decompress data; zlib not available

执行命令echo $?验证安装是否成功,输出为0说明安装成功

备注3：

执行的是 ./configure，则安装后可执行文件默认放在/usr /local/bin，库文件默认放在/usr/local/lib，配置文件默认放在/usr/local/include，其它的资源文件放在/usr /local/share。

执行的是./configure --prefix=/usr/local/python3.7.6，则可执行文件放在/usr /local/python3.7.6/bin，库文件放在/usr/local/python3.7.6/lib，配置文件放在/usr/local/python3.7.6/include，其它的资源文件放在/usr /local/python3.7.6/share

#### 更新pip

```shell
pip3 install --upgrade pip
```

查看版本

```shell
pip –V
```

#### 更换python版本链接(注意整体更换，目前尚未使用)

基本原理：将原有的python链接指向新的版本

1)  配置环境变量

```shell
vi ~/.bashrc
#配置python
export PYTHON37_HOME=/usr/local/python3.7.6
export PATH=$PYTHON37_HOME/bin:$PATH
```

2)  修改默认链接

source ~/.bashrc命令使配置生效。执行echo命令，查看是否配置成功：

```shell
source ~/.bashrc
echo $PYTHON37_HOME
```

修改python环境变量链接：备份->删除原有链接->建立新的链接

```shell
cp /usr/bin/python /usr/bin/python.bak 
rm -f /usr/bin/python
ln -s /usr/local/python3.7.6/bin/python3.7 /usr/bin/python
python -V
```

```shell
cp -f /usr/bin/pip3 /usr/bin/pip3.bak
rm -f /usr/bin/pip3
```

```shell
ln -s /usr/local/python3.7.6/bin/pip3 /usr/bin/pip3
```

```shell
pip3 -V
```

 Python的一大优势就是拥有庞大的第三方支持库，而要使用这些库，就离不开Python包管理工具pip，所以我们现在马上下载一个。

查询pip版本

```shell
pip3 –V
```

默认使用python3.5的版本：

```shell
pip 9.0.1 from /home/microblog/venv/lib/python3.5/site-packages (python 3.5)
```



### python验证

进入python3.7.6

```shell
python
import ssl
import _ssl
```

没有出现No module named _ssl, 说明安装链接成功ssl.

Ctrl+z可退出Python

#### pip换源（未验证有效性）

在/root目录或者/home/xxx目录下:

```shell
mkdir ~/tools/.pip
vim ~/tools/.pip/pip.conf
```

vim打开输入:

```shell
[global]
index-url=http://mirrors.aliyun.com/pypi/simple/
 
[install]
trusted-host=mirrors.aliyun.com
```

### **其他问题**

##### GCC编译环境安装(如果需要)

说明没有安装合适的编译器。这时，需要安装/升级 gcc 及其它依赖包。

```shell
sudo apt-get install make gcc
```

 

##### **zlib****模块安装(如果需要)**

先去http://www.zlib.net/下载最新版本的zlib源码文件

```shell
wget http://www.zlib.net/zlib-1.2.11.tar.gz
```

安装zlib:

```shell
tar xzvf zlib-1.2.11.tar.gz
cd zlib-1.2.11
./configure
make
make install
```

zlib安装完后，libz.a在/usr/local/lib/,zlib.h文件在/usr/include （opensuse中zlib.h默认放在/usr/local/include/中）

## 安装python2.7.13及相关环境

### 下载安装Python2.7

```shell
wget https://www.python.org/ftp/python/2.7.13/Python-2.7.13.tgz
tar -xzvf Python-2.7.13.tgz
cd Python-2.7.13
./configure -prefix=/usr/local/python2.7.13 --with-ssl
make
make install
```



### 配置python

```shell
vi ~/.bashrc
```

\#配置python2.7

```shell
export PYTHON27_HOME=/usr/local/python2.7.13
export PATH=$PYTHON27_HOME/bin:$PATH
```

 

```shell
source ~/.bashrc
echo $PYTHON27_HOME
```

 

```shell
cp /usr/bin/python2 /usr/bin/python2.bak 
rm -f /usr/bin/python2
ln -s /usr/local/python2.7.13/bin/python2.7 /usr/bin/python2
python2 -V
```



#### 安装pip2

下载地址：[https://pypi.python.org/pypi/pip#downloads](https://link.jianshu.com?t=https%3A%2F%2Fpypi.python.org%2Fpypi%2Fpip%23downloads)

```shell
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python get-pip.py
```



#### 配置pip2

安装python2的pip

```shell
cp -f /usr/bin/pip2 /usr/bin/pip2.bak
rm -f /usr/bin/pip2
ln -s /usr/local/python2.7.13/bin/pip2 /usr/bin/pip2
pip2 -V
```



## 虚拟环境使用

### 配置虚拟环境

安装virtualenv virtualenvwrapper

```shell
pip3 install virtualenv virtualenvwrapper
```

创建链接

```shell
rm /usr/bin/virtualenvwrapper.sh
ln -s /usr/local/python3.7.6/bin/virtualenvwrapper.sh /usr/bin/virtualenvwrapper.sh
rm /usr/bin/virtualenv
ln -s /usr/local/python3.7.6/bin/virtualenv /usr/bin/virtualenv
```

建立web端的虚拟环境

修改bash文件 `vim /etc/bash.bashrc`, 输入:

```shell
export WORKON_HOME=/home/web/web_venv/.venv
source /usr/bin/virtualenvwrapper.sh
VIRTUALENVWRAPPER_PYTHON=/usr/local/python3.7.6/bin/python3.7
```

bash生效

```shell
source /etc/bash.bashrc
```

 

### 启动虚拟环境

手动切换虚拟环境：

```shell
source web_venv/.venv/flask_env/bin/activate
```

Python3创建虚拟环境(创建成功后会自动进入虚拟环境)

```shell
mkvirtualenv -p python3 flask_env
```

l 退出虚拟环境

```shell
deactivate
```

l 进入虚拟环境

```shell
workon flask_env
```

l 查看所有虚拟环境

```shell
workon
```

l 删除虚拟环境

```shell
rmvirtualenv 虚拟环境名称
```



## 常用命令

### 查看端口

典型问题：Bind for 0.0.0.0:9000 failed: port is already allocated

查看端口：

```shell
netstat | grep 9000
```

查看线程：

```shell
docker ps
```

### 依赖安装

典型问题：dpkg: warning: files list file for package

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/04/20200304160035.png)

例如安装php，出现如下问题

```
sudo apt-get install php php-xml
```

可使用如下方式安装依赖关系包

```
for package in $( apt-get install php php-xml 2>&1 | grep "warning: files list file for package '" | grep -Po "[^'\n ]+'" | grep -Po "[^']+"); do apt-get install --reinstall "$package"; done
```

注意事项：

1.  该脚本运行时间取决于warning数量，需要时间较长，如果遇到问题会停下来，需要运行remove后再次运行；

2.  该warning有时候出现，再次安装不出现，可先删除php；安装如果卡住了，可使用删除和重新安装来看原因；

    ```
    sudo apt-get remove php php-xml
    sudo apt-get install php php-xml
    ```

### 找不到模块

典型问题：ModuleNotFoundError: No module named 'ConfigParser'

![](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/03/04/20200304160130.png)

分析方法：

在Python2中`import ConfigParser`

在Python3中`import configparser`

即此处调用的python版本错误，代码为python2的，需要替换成python3的