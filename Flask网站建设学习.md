# Flask网站建设学习

参考教程：

1.  [Python基本语法学习(推荐)](https://github.com/jackfrued/Python-100-Days)

2.  Flask网站教程：

    1) [html与python参数传递](https://www.yty99.cn/?p=61)

    2) [Hello World配置版](https://www.jianshu.com/p/cc90a14856c5)

3.  视频教程：[B站 小甲鱼的视频](https://www.bilibili.com/video/av4050443/)

4.  网页调用python方案：[wooey](https://wooey.herokuapp.com/)

    

    

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



# Python：flask框架下前后端的数据交互

### html传递数据到python

参考视频：[一晚上学会flask你信不信](https://www.bilibili.com/video/av80320225?from=search&seid=4210633810962912541)

使用表单form进行数据传递：

前端

```
<!DOCTYPE html>
<html lang="zh-cn">
    <head>
        <meta charset="utf-8">
        <title>HelloWorld</title>
    </head>
    <body>
        <h1>login</h1>
        <form action="/login" method="POST">
            用户名<input type="text" name="username"> <br/>
            密码<input type="password" name="pwd"><br/>
            <input type="submit" value="登陆"><br/>
            {{ msg }}
        </form>
    </body>
</html>
```

python

```
# 使用render_template这个函数渲染模板
from flask import Flask,render_template,request

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("login.html")

@app.route("/login",methods=['POST'])
def login():
    username = request.form.get("username")
    password = request.form.get("pwd")
    if username == "ajax" and password == "123":
        return "成功 "
    else:
        return render_template("login.html", msg="登陆失败")

if __name__ == "__main__":
    app.run()
```



参考1：[参考文档](https://blog.csdn.net/qq_42780289/article/details/91129147?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)

参考2：[Python Flask前后端Ajax交互的方法示例](http://www.word666.com/jiaoben/176603.html)



python传递数据到前端显示(例子已验证)：

[使用ajax完成python flask前端与后台数据的交互](https://blog.csdn.net/omodao1/article/details/83049960)

## flask通过template向javascript传递数据的方法

方法一：js端处理

其实很简单，在渲染模板时传入变量

```
@app.route('/')
def hello():
    variable = {'username': 'Pang', 'site': 'stackoverflow.com'}
    return render_template('template.html', variable=variable）
```

只需在模板中定义script标签

```
<script type="text/javascript">
var someJavaScriptVar = '{{ variable|tojson }}';
</script>
```

方法二：python端处理

```
    List = ['列表1', '列表2']
    Dict = {'键1': '值1', '键2': '值2'}
    return render('home.html', {
            'List': json.dumps(List),
            'Dict': json.dumps(Dict)
        })
————————————————
版权声明：本文为CSDN博主「Agly_Charlie」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/Agly_Clarlie/article/details/50551807
```



```
  <script type="text/javascript">
    var List = {{ List|safe }};//列表
    var Dict = {{ Dict|safe }};//字典
    </script>

```



## google Map使用

第一步：

GoogleMap服务启用，需要有GAE的收费账号，启用对应的Google API服务

https://cloud.google.com/console/google/maps-apis/overview

第二步：

参考代码：https://github.com/flask-extensions/Flask-GoogleMaps

代码最后要教程的链接



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

### 常见问题

#### jinja2.exceptions.TemplateNotFound: 

问题1：

Flask读取模版是在app.py下的`templates`下

问题2：
  没有`templates`文件夹，因为默认情况下，Flask在程序文件夹中的`templates`子文件夹中寻找模板。



作者：白帽札记
链接：https://www.jianshu.com/p/8df0fbe4e64e
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

## 名词解释

### Ajax

这个术语源自描述从基于 Web 的应用到基于数据的应用。

Ajax 不是一种新的编程语言，而是一种用于创建更好更快以及交互性更强的Web应用程序的技术。

使用 JavaScript 向服务器提出请求并处理响应而不阻塞用户核心对象[XMLHttpRequest](https://baike.baidu.com/item/XMLHttpRequest)。通过这个对象，您的 JavaScript 可在不重载页面的情况与 Web 服务器交换数据，即在不需要刷新页面的情况下，就可以产生局部刷新的效果。

Ajax不需要任何浏览器插件，但需要用户**允许[JavaScript](https://baike.baidu.com/item/JavaScript)在浏览器上执行**。就像[DHTML](https://baike.baidu.com/item/DHTML)应用程序那样，Ajax应用程序必须在众多不同的浏览器和平台上经过严格的测试。随着Ajax的成熟，一些简化Ajax使用方法的程序库也相继问世。同样，也出现了另一种辅助程序设计的技术，为那些不支持[JavaScript](https://baike.baidu.com/item/JavaScript)的用户提供替代功能。

### JavaScript 

JavaScript（简称“JS”） 是一种具有[函数](https://baike.baidu.com/item/函数/301912)优先的[轻量级](https://baike.baidu.com/item/轻量级/22359343)，解释型或即时编译型的[编程语言](https://baike.baidu.com/item/编程语言/9845131)。虽然它是作为开发Web页面的[脚本语言](https://baike.baidu.com/item/脚本语言/1379708)而出名的，但是它也被用到了很多非浏览器环境中，JavaScript 基于原型[编程](https://baike.baidu.com/item/编程/139828)、多范式的动态脚本语言，并且支持[面向对象](https://baike.baidu.com/item/面向对象/2262089)、命令式和声明式（如[函数式编程](https://baike.baidu.com/item/函数式编程/4035031)）风格。 [1]

JavaScript是一种属于网络的脚本语言,已经被广泛用于Web应用开发,常用来为网页添加各式各样的动态功能,为用户提供更流畅美观的浏览效果。通常JavaScript脚本是通过嵌入在HTML中来实现自身的功能的。 [5] 

1.  是一种解释性脚本语言（代码不进行[预编译](https://baike.baidu.com/item/预编译)）。 [6] 
2.  主要用来向[HTML](https://baike.baidu.com/item/HTML)（[标准通用标记语言](https://baike.baidu.com/item/标准通用标记语言)下的一个应用）页面添加交互行为。 [6] 
3.  可以直接嵌入HTML页面，但写成单独的[js](https://baike.baidu.com/item/js/10687961)文件有利于结构和行为的[分离](https://baike.baidu.com/item/分离)。 [6] 
4.  跨平台特性，在绝大多数浏览器的支持下，可以在多种平台下运行（如[Windows](https://baike.baidu.com/item/Windows)、[Linux](https://baike.baidu.com/item/Linux)、[Mac](https://baike.baidu.com/item/Mac/173)、[Android](https://baike.baidu.com/item/Android/60243)、[iOS](https://baike.baidu.com/item/iOS/45705)等）。
5.  Javascript脚本语言同其他语言一样，有它自身的基本数据类型，表达式和[算术运算符](https://baike.baidu.com/item/算术运算符/9324947)及程序的基本程序框架。Javascript提供了四种基本的数据类型和两种特殊数据类型用来处理数据和文字。而变量提供存放信息的地方，表达式则可以完成较复杂的信息处理。