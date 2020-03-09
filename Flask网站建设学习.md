# Flask网站建设学习

参考教程：

1.  [Python基本语法学习(推荐)](https://github.com/jackfrued/Python-100-Days)

2.  Flask网站教程：

    1) [html与python参数传递](https://www.yty99.cn/?p=61)

    2) [Hello World配置版](https://www.jianshu.com/p/cc90a14856c5)

3.  视频教程：B站 小甲鱼的视频

### 开发环境

python版本：3.7.6（可支持GCA）

开发工具：pycharm2019

虚拟环境：Anaconda

### Flask程序目录结构

Flask 项目有4个顶级文件夹：

-   app ——(本例中是 jbox）Flask 程序保存在此文件夹中
-   migrations ——包含数据库迁移脚本（安装了 flask-migrate 后自动生成）
-   tests ——单元测试放在此文件夹下
-   venv ——Python 虚拟环境(Anaconda无)

同时还有一些文件：

-   requirements.txt —— 列出了所有的依赖包，以便于在其他电脑中重新生成相同的环境
-   config.py 存储配置
-   manage.py 启动程序或者其他任务
-   gun.conf Gunicorn 配置文件

## 原理

### 路由和视图函数

客户端把请求发给 Web 服务器，Web 服务器再把请求发给 Flask 程序实例，Flask 程序实例需要知道每个 URL 请求要运行哪些代码，所以保存了一个 URL 到 Python 函数的映射关系。处理 URL 和函数之间关系的程序称为路由，这个函数称为视图函数。例如：

```python
@app.route('/')
def index():
    return '<h1>Hello World</h1>'
```

#### 蓝本管理路由



## 要点：

### app.router('/')是app.add_url_rule的语法糖

```
@app.route('/')
def index():
    return "HelloWorld"
```

等效

```
def index():
    return "HelloWolrd"
app.add_url_rule('/',view_func = index)
```



### Jinja2模板使用：

Flask 使用了 Jinja2 引擎来渲染模板，模板文件都放在 templates 文件夹下，并且只能命名为 templates，否则 Jinja2 会抛出 TemplageNotFound 异常

### Jinja2

Jinja2是基于[python](https://baike.baidu.com/item/python/407313)的[模板引擎](https://baike.baidu.com/item/%E6%A8%A1%E6%9D%BF%E5%BC%95%E6%93%8E/907667)，功能比较类似于于[PHP](https://baike.baidu.com/item/PHP/9337)的[smarty](https://baike.baidu.com/item/smarty/7270424)，[J2ee](https://baike.baidu.com/item/J2ee)的[Freemarker](https://baike.baidu.com/item/Freemarker)和[velocity](https://baike.baidu.com/item/velocity/1398152)。 它能完全支持[unicode](https://baike.baidu.com/item/unicode/750500)，并具有集成的沙箱执行环境，应用广泛。jinja2使用[BSD](https://baike.baidu.com/item/BSD)授权。

#### if控制

在Jinja2中控制语句（if、for）使用 “{%” 和 “%}” 括起来，由 “[” 和 “]”括起来的部分代表是可选的，因为HTML会忽略源文件中的空白，所以无法使用缩进来确定 if 语句的结尾，需要使用 “{% endif %}” 表示 if 语句的结尾。

```jinja2
{% if 条件1 %}
    语句块1
[ {% elif 条件2 %} ]
    [ 语句块2 ]
...
[ {% else %} ]
    [ 语句块3 ]
{% endif %}
```

`if` 后面的条件可以写类似Python的条件表达式，具体的细节可以参考[官方文档](http://docs.jinkan.org/docs/jinja2/templates.html#if)。

#### for循环

Jinja2提供了 `for` 语句用来循环的渲染某一个语句，当我们需要动态的生成一个列表或者表格的时候，使用 `for` 循环可以化简我们的工作量：

Jinja2还内置了一些循环变量，可以在循环中访问它们：

```
# loop.index                当前循环迭代的次数（从 1 开始）
# loop.index0               当前循环迭代的次数（从 0 开始）
# loop.revindex             到循环结束需要迭代的次数（从 1 开始）
# loop.revindex0            到循环结束需要迭代的次数（从 0 开始）
# loop.first                如果是第一次迭代，为 True 。
# loop.last                 如果是最后一次迭代，为 True 。
# loop.length               序列中的项目数。
# loop.cycle                在一串序列间期取值的辅助函数。
```



#### 过滤器



#### 模板继承





### 常用扩展工具

flask-script 可以自定义命令行命令，用来启动程序或其它任务；flask-sqlalchemy 用来管理数据库的工具，支持多种数据库后台；flask-migrate 是数据库迁移工具，该工具命令集成到 flask-script 中，方便在命令行中进行操作。