# Linux常用命令

| 功能                        | 命令                                                         |
| --------------------------- | ------------------------------------------------------------ |
| 版本查询                    | 系统版本：lsb-release-ds<br/>Python版本：python-V<br/>Pip版本：pip-V<br/>php版本：php–v<br/>nginx版本：nginx-v |
| /home下搜索pip文件夹        | find/home-namepip                                            |
| 软链接                      | ln-sv/usr/local/python/bin/pip/usr/bin/pip                   |
| 查看某个目录软连接          | ls-l/usr/local/bin                                           |
| 查看默认的配置路径          | ls-l                                                         |
| 查看PATH路径                | echo$PATH                                                    |
| 查看程序路径                | whichpython                                                  |
| 当前所在路径                | pwd                                                          |
| 文件解压                    | tar-axfpip-1.5.4.tar.gz                                      |
| 从shell（终端）中退出python | 方法1：快捷键：ctrl+Z方法2：exit()                           |
| 查看python3版本             | 1.默认python版本查询python-V或python–version2.python3版本查询python3–version |
| 删除非空文件夹              | rm-rxxx                                                      |
| 查看硬盘使用情况            | 查看当前目录df-h查看当前目录每个文件夹的情况du--max-depth=1-h |
| 文件重命名                  | sudomv/var/lib/dpkg/info/var/lib/dpkg/info.bak               |

## 软件安装

| 功能       | 命令                                                         |
| ---------- | ------------------------------------------------------------ |
| 安装/卸载  | apt-get例如：sudoapt-getinstallpython3-pip<br/>sudoapt-getinstallphpphp-xml<br/>sudoapt-getremovephpphp-xml |
| Pip安装    | pipinstall<package-name>                                     |
| 卸载       | `sudoapt-getremovelighttpdphp5-cgi``whichlighttpd`           |
| 依赖安装   | `sudoapt-getbuild-depphpphp-xml`                             |
| 系统更新   | aptupdate&&aptupgrade-y                                      |
| 更新插件库 | `apt-getupdate`                                              |

依赖包安装

```
forpackagein$(apt-getinstallphpphp-xml2>&1|grep"warning:fileslistfileforpackage'"|grep-Po"[^'\n]+'"|grep-Po"[^']+");doapt-getinstall--reinstall"$package";done`
```



## VIM命令

| 功能         | 命令 |
| ------------ | ---- |
| 查看链接     | ls-l |
| 进入编辑状态 | i    |
| 删除一行     | dd   |
| 不保存退出   | :q!  |
| 保存退出     | :wq  |

## 网络命令

| 功能                 | 命令                                                         |
| -------------------- | ------------------------------------------------------------ |
| 进入编辑状态         | i                                                            |
| 删除一行             | dd                                                           |
| 不保存退出           | :q!                                                          |
| 保存退出             | :wq                                                          |
| 查询和杀死进程       | 查询当前进行：ps<br/>PIDTTYTIMECMD820pts/000:00:00bash1137pts/000:00:00python1138pts/000:00:00ps<br/>杀死进程python：`kill-s91137` |
| 查看端口             | 查看端口：netstat\|grep9000<br/>查看线程：dockerps<br/>查看docker端口情况：`netstat-lntp|grepdockerd`<br/>查看进程：`psaux|grepdockerd=` |
| 杀死进程             | 杀死进程：killall-9nginx                                     |
| 查看端口             | 端口查询：netstat-ntpl                                       |
| 设置开机服务自动运行 | 开启docker服务并设置开机启动<br/>systemctlstartdocker.service<br/>systemctlenabledocker.service |

## Xshell

### Xshell中使用vim的粘贴

Vim的编辑模式中，还有一个Paste模式，在该模式下，可将文本原本的粘贴到Vim中，以避免一些格式错误。通过“:setpaste”和“:setnopaste”进入和退出该模式。

可参考文档，提供多种VIM粘贴方式：

https://blog.joefom.com/archives/225



## 附录

### [linux中wget、apt-get、yumrpm区别](https://www.cnblogs.com/llxx07/p/7744355.html)

wget类似于迅雷，是一种下载工具，

通过HTTP、HTTPS、FTP三个最常见的TCP/IP协议下载，并可以使用HTTP代理名字是WorldWideWeb”与“get”的结合。



yum:是redhat,centos系统下的软件安装方式，基于Linux，

全称为YellowdogUpdater,Modified，

是一个在Fedora和RedHat以及CentOS中的Shell前端软件包管理器

基于RPM包管理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软件包。



rpm:软件管理;

redhat的软件格式rpmr=redhatp=packagem=management

用于安装卸载.rpm软件串联下：

使用wget下载一个rpm包,然后用rpm-ivhxxx.rpm安装这个软件，嫌麻烦的话，就可以直接用yuminstallsqoop来自动下载和安装依赖的rpm软件。



apt-get是ubuntu下的一个软件安装方式，它是基于debain。