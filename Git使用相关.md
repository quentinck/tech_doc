# Git使用相关

## 基本使用



### GAE Github

参考文章：https://www.runoob.com/git/git-basic-operations.html

```shell
cd ~
git clone https://github.com/quentinck/garminexport.git
cd garminexport
```

git设置

```
git config --global user.name 'quentin'
git config --global user.email quentin2052ck@gmail.com
```

git添加文件

```shell
git add xxx
```

git查看状态

```shell
git status
git commit -m 'GAE run ok'
```





### pycharm push to Github

VCS->Git->push

参考：https://www.jianshu.com/p/94aafbe82dc7



## 常见问题

### Github:No supported authentication methods available(server sent publickey)

解决办法：https://www.cnblogs.com/nsky/p/8847610.html

注意区分：TortoiseGit和Git，TortoiseGit为Git的GUI客户端，实际服务是Git提供，所以Git也可用于pycharm等IDE。

### 使用tortoisegit访问github

使用https协议访问即可

参考文档：https://blog.csdn.net/winy_lm/article/details/80452590