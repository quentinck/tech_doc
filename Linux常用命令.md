# Linux常用命令



### 安装

```
sudo apt-get install php php-xml
sudo apt-get remove php php-xml
```

### 更新系统

```
apt update && apt upgrade -y
```

### 查看链接路径

可使用ls -l查看默认的配置路径

```
ls -l
```

典型问题：Bind for 0.0.0.0:9000 failed: port is already allocated

创建链接

```
sudo ln -s /usr/local/python3.7.6/ /usr/bin/python
```

### 文件重命名

```
sudo mv /var/lib/dpkg/info /var/lib/dpkg/info.bak
```

### 查看端口

查看端口：

```shell
netstat | grep 9000
```

查看线程：

```shell
docker ps
```

### 