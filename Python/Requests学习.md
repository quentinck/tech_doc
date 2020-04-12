

# Requests学习

[官方网站](http://www.python-requests.org)

## Requests入门

![image-20200405093442773](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405093444.png)

![image-20200405100817827](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405100819.png)

### Requests库的get方法

![image-20200405093912127](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405093913.png)

![image-20200405094021650](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405094023.png)

其他六个方法都是通过调用requests方法来实现的

![image-20200405094036669](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405094038.png)

### Response对象

![image-20200405094138490](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405094140.png)

![image-20200405094204201](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405094205.png)

![image-20200405094250356](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405094251.png)

基本访问流程

![image-20200405094335673](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405094336.png)

![image-20200405094432554](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405094434.png)

### 爬取网页的通用代码框架

#### Requests库的异常

![image-20200405094607327](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405094609.png)

![image-20200405094628755](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405094630.png)

![image-20200405094706403](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405094707.png)

#### HTTP协议

![image-20200405094822823](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405094824.png)

![image-20200405094833664](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405094838.png)

![image-20200405094853268](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405094858.png)

![image-20200405094912094](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405094913.png)

![image-20200405094948324](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405094949.png)

![image-20200405095024183](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405095025.png)

#### HTTP协议与Requests库方法对应

![image-20200405095044903](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405095046.png)

##### head()

![image-20200405095130929](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405095132.png)

##### post()

![image-20200405095156313](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405095157.png)

![image-20200405095229523](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405095230.png)

##### put()

![image-20200405095302855](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405095304.png)

### Request库的主要方法

![image-20200405095548047](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405095549.png)

![image-20200405095609735](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405095610.png)

#### 参数：params

![image-20200405095700282](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405095701.png)

#### 参数：data

![image-20200405095753182](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405095754.png)

#### 参数：json

![image-20200405095924173](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405095925.png)

#### 参数：headers

可模拟使用chrome 10版本向服务器请求

![image-20200405095946195](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405095947.png)

#### 参数：cookies/auth

![image-20200405100041217](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405100043.png)

#### 参数：files

![image-20200405100059512](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405100102.png)

#### 参数：timeout

![image-20200405100115623](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405100116.png)

#### 参数：proxies

防止对爬虫的逆追踪

![image-20200405100224665](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405100226.png)

#### 参数：高级功能

![image-20200405100302543](upload/image-20200405100302543.png)

#### 总结

![image-20200405100352982](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405100354.png)

![image-20200405100412867](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405100414.png)

![image-20200405100434006](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405100435.png)

![image-20200405100444865](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405100446.png)

![image-20200405100502649](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405100504.png)

![image-20200405100512010](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405100514.png)

![image-20200405100523280](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405100524.png)



## 网络爬虫的协议

### 网络爬虫的尺寸

![image-20200405101253380](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405101254.png)

![image-20200405101329109](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405101331.png)

![image-20200405101347524](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405101348.png)

![image-20200405101403657](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405101404.png)

![image-20200405101417495](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405101418.png)

![image-20200405101504681](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405101506.png)

### Robots协议

![image-20200405101551590](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405101552.png)

![image-20200405101837281](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405101838.png)

![image-20200405101858622](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405101859.png)

![image-20200405102124848](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405102125.png)

### Robots协议的遵守方式

![image-20200405102245618](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405102247.png)

![image-20200405102603426](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405102604.png)

## 爬取实例

### 实例1：京东商品

![image-20200405102816671](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405102817.png)

```python
import requests
url = 'https://item.jd.com/100004546721.html'
def test_jd():
    try:
        r = requests.get(url)
        r.raise_for_status()
        r.encoding = r.apparent_encoding
        print(r.text[:1000])
    except:
        print("爬取失败")

test_jd()
```

### 实例2：亚马逊商品

爬取失败的分析方法

![image-20200405104154895](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405104156.png)

![image-20200405104208397](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405104210.png)

修改浏览器信息

```
kv = {'user-agent': 'Mozilla/5.0'}
r = requests.get(url, headers = kv)
```

![image-20200405104302315](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405104303.png)

![image-20200405104318258](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405104319.png)

### 实例3：百度/360搜索关键词提交

![image-20200405104433925](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405104435.png)

![image-20200405104624581](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405104625.png)

![image-20200405104643318](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405104644.png)

![image-20200405104703125](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405104706.png)

### 实例4：网络图片的爬取和存储

![image-20200405104802457](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405104803.png)

![image-20200405104954883](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405104955.png)

![image-20200405105019795](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405105021.png)

### 实例5：IP地址归属地的自动查询

![image-20200405105229337](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405105230.png)

![image-20200405105302568](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405105303.png)

![image-20200405105328276](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405105329.png)



### 总结

![image-20200405105450399](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405105451.png)

## 网络爬虫与信息提取Beautiful Soup

![image-20200405114153373](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114154.png)

![image-20200405110120508](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405110121.png)

![image-20200405112812974](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405112814.png)

![image-20200405112858705](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405112900.png)

### 提取的分析方法

![image-20200405105536770](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405105538.png)

pip install beautifulsoup4

![image-20200405105709147](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405105710.png)

![image-20200405105718970](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405105720.png)

手动获得链接源代码

![image-20200405105814068](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405105815.png)

requests库获得源代码：

![image-20200405105903469](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405105904.png)



![image-20200405110014940](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405110016.png)

### Beautiful Soup库的基本元素

![image-20200405110227103](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405110228.png)

![image-20200405110654746](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405110656.png)

![image-20200405110727011](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405110728.png)

![image-20200405110833604](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405110834.png)

![image-20200405110932510](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405110933.png)

![image-20200405110952817](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405110953.png)

```
from bs4 import BeautifulSoup
r = requests.get("http://python123.io/ws/demo.html")
demo = r.text
soup = BeautifulSoup(demo, "html.parser")
soup.title
```

![image-20200405111958571](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405111959.png)

![image-20200405112125709](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405112127.png)

![image-20200405112506984](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405112508.png)

![image-20200405112611034](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405112612.png)

![image-20200405112720921](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405112722.png)

### 基于bs4库的HTML内容遍历方法

![image-20200405113014678](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405113015.png)

![image-20200405113025308](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405113026.png)

![image-20200405113103275](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405113104.png)

#### 标签树的下行遍历

![image-20200405113152650](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405113153.png)

实例

![image-20200405113302991](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405113305.png)

![image-20200405113337682](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405113338.png)

![image-20200405113351545](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405113352.png)

#### 标签数的上行遍历

![image-20200405113407464](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405113408.png)

![image-20200405113505708](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405113506.png)

#### 标签数的平行遍历

![image-20200405113535618](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405113536.png)

![image-20200405113612072](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405113613.png)

![image-20200405113741500](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405113742.png)

#### 总结

![image-20200405113816148](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405113817.png)

### 基于bs4库的HTML格式化和编码

所有支持的编码默认为utf-8

![image-20200405113949823](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405113952.png)

![image-20200405114032395](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114036.png)



## 信息的标记

![image-20200405114319481](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114320.png)

![image-20200405114339486](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114341.png)

![image-20200405114351601](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114352.png)

![image-20200405114407034](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114408.png)

#### XML/JSON/YAML比较

![image-20200405121059679](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405121101.png)

##### XML

![image-20200405114430427](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114431.png)

![image-20200405114443045](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114444.png)

![image-20200405114509723](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114510.png)

##### JSON

![image-20200405114607211](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114608.png)

![image-20200405114627070](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114628.png)

![image-20200405114645290](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114646.png)

![image-20200405114654801](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114655.png)

##### YAML

![image-20200405114829771](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114832.png)

![image-20200405114935731](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114937.png)

利用缩进来表达

![image-20200405114851167](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114852.png)

![image-20200405114901508](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114902.png)

![image-20200405114917157](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405114918.png)

##### 三种信息标记的比较

![image-20200405115032305](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405115034.png)

![image-20200405115045472](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405115046.png)

![image-20200405115058349](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405115059.png)

![image-20200405115205374](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405115207.png)

HTML格式属于XML格式类别

![image-20200405115308300](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405115309.png)

### 信息提取的一般方法

![image-20200405121153381](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405121154.png)

![image-20200405115450009](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405115451.png)

![image-20200405115513981](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405115515.png)

![image-20200405115637212](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405115638.png)

#### 实例

![image-20200405115708413](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405115709.png)

![image-20200405115754994](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405115755.png)

### 基于bs4库的HTML内容查找方法

![image-20200405120159175](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405120200.png)

#### name参数

![image-20200405120234350](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405120235.png)

搜索'a'标签

![image-20200405120259799](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405120301.png)打印所有标签

![image-20200405120349364](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405120350.png)

正则表达式搜索

![image-20200405120435706](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405120436.png)

#### attrs参数

![image-20200405120510876](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405120511.png)

属性需要精确的信息

![image-20200405120600248](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405120601.png)

也可以引入正则表达式

![image-20200405120630830](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405120632.png)

#### recursive参数

![image-20200405120651852](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405120653.png)

![image-20200405120733334](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405120734.png)

#### string参数

![image-20200405120746687](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405120749.png)

需精确输入

![image-20200405120813666](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405120814.png)

使用正则表达式

![image-20200405120837573](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405120838.png)

![image-20200405120910641](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405120911.png)

#### 7个扩展方法

参数与<>.find_all()方法一致

![image-20200405120933181](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405120934.png)

### 实例1：定向爬虫

http://www.zuihaodaxue.cn/zuihaodaxuepaiming2019.html

![image-20200405121427417](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405121428.png)

![image-20200405143431946](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405143433.png)

可行性确定：确定html信息是动态提取还是静态的，这里针对静态信息

1.  打开网页->查看源代码

    ![image-20200405141507567](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405141508.png)

    

2.  查看Robots协议

    ![image-20200405121712254](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405121713.png)

3.  需求

    ![image-20200405121737633](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405121739.png)

4.  程序的结构设计

    ![image-20200405121844257](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405121848.png)

5.  编写代码

```python
import requests
from bs4 import BeautifulSoup
import bs4

# 获取url信息,输出url的内容
def getHTMLText(url):
    try:
        r = requests.get(url, timeout=30)
        r.raise_for_status()
        r.encoding = r.apparent_encoding
        return r.text
    except:
        return "爬取失败"

# 将html页面放到list列表中
def fillUnivList(ulist, html):
    soup = BeautifulSoup(html, "html.parser")
    for tr in soup.find('tbody').children:
        if isinstance(tr, bs4.element.Tag):
            tds = tr('td')
            ulist.append([tds[0].string, tds[1].string, tds[2].string])
    pass

# 将ulist信息打印出来,num定义需要打印的梳理
def printUnivList(ulist, num):
	tplt = "{0:^10}\t{1:{3}^10}\t{2:^10}"#使用format的第三个参数进行填充
	print(tplt.format("排名", "学校名称", "总分", chr(12288)))
    for i in range(num):
        u = ulist[i]
        print(tplt.format(u[0], u[1], u[2]), chr(12288))

def main():
    uinfo = []
    url = 'http://www.zuihaodaxue.cn/zuihaodaxuepaiming2019.html'
    html = getHTMLText(url)
    fillUnivList(uinfo, html)
    printUnivList(uinfo, 20)  # 列出20所学校信息

main()
```



## 常用方法

### 爬取的头

```
kv = {"User-Agent":"Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.87 Safari/537.36"}
```

### format方法打印

![image-20200405140126137](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405140129.png)

打印实例：

```
print("{:^10}\t{:^6}\t{:^10}".format("排名", "学校名称", "总分"))
```

打印结果

```
    排名    	 学校名称 	    总分   
```



### 中文输出对齐问题

![image-20200405134359346](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405134402.png)

![image-20200405142401332](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405142402.png)

优化前：

```
print("{:^10}\t{:^6}\t{:^10}".format("排名", "学校名称", "总分"))
```

优化后：

```
tplt = "{0:^10}\t{1:{3}^10}\t{2:^10}"#使用format的第三个参数进行填充
print(tplt.format("排名", "学校名称", "总分", chr(12288)))
```

## 正则表达式

### 正则表达式的概念

![image-20200405143941243](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405143942.png)

![image-20200405144241472](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405144242.png)

![image-20200405143909720](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405143911.png)

![image-20200405143959099](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405144000.png)

![image-20200405144100762](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405144101.png)

#### 总结

![image-20200405144153173](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405144154.png)

![image-20200405144224695](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405144225.png)

![image-20200405144254537](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405144255.png)

### 正则表达式的语法

![image-20200405144400484](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405144401.png)

![image-20200405144421895](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/05/20200405144423.png)



## 爬虫代码

参考：https://blog.csdn.net/qq_43764365/article/details/103539728

1.注意修改代码中的driver_path路径为：

```
driver_path = "C:/Users/quent/AppData/Local/Google/Chrome/Application/chromedriver.exe"
```

同时需要下载chromedriver.exe到此路径中

```
from selenium import webdriver
from time import sleep
import re
import os
 
 
# 搜索商品
def search_products():
    # 输入商品名字
    driver.find_element_by_xpath('//*[@id="key"]').send_keys(keyword)
    # 点击搜索
    driver.find_element_by_xpath('//*[@class="form"]/button').click()
    sleep(10)
    token = driver.find_element_by_xpath('//*[@id="J_bottomPage"]/span[2]/em[1]/b').text
    # 0代表所有匹配到的数字
    token = int(re.compile('(\d+)').search(token).group(1))
    # 返回总页数
    return token
 
 
# 下拉下滑条，加载数据
def drop_down():
    for x in range(1, 11, 2):
        sleep(1)
        j = x / 10
        js = 'document.documentElement.scrollTop = document.documentElement.scrollHeight * %f' % j
        driver.execute_script(js)
 
 
# 获取商品信息
def get_product():
    lis = driver.find_elements_by_xpath('//*[@class="gl-warp clearfix"]/li[@class="gl-item"]')
    for li in lis:
        price = li.find_element_by_xpath('.//div[@class="p-price"]/strong/i').text + '元'
        info = li.find_element_by_xpath('.//div[@class="p-name"]/a/em').text + li.find_element_by_xpath(
            './/div[@class="p-name"]/a').get_attribute('title')
        p_commit = li.find_element_by_xpath('.//div[@class="p-commit"]/strong/a').text
        p_shopnum = li.find_element_by_xpath('.//div[@class="p-shopnum"]/*').text
        p_img = li.find_element_by_xpath('.//div[@class="p-img"]/a/img').get_attribute('src')
        print(info, price, p_commit, p_shopnum, p_img, sep='|')
 
 
# 翻页
def next_page():
    token = search_products()
    num = 1
    while (num != token):
        driver.get('https://search.jd.com/Search?keyword={}&page={}'.format(keyword, 2 * num - 1))
        driver.implicitly_wait(10)
        num += 1
        drop_down()
        get_product()
 
 
if __name__ == "__main__":
    keyword = input('输入你想查找的商品名字:')
    driver_path = os.path.abspath(os.path.join(os.getcwd(), "..")) + "/Drive/chromedriver.exe"
    driver = webdriver.Chrome(driver_path)
    # 窗口最大化，防止数据丢失
    driver.maximize_window()
    driver.get('https://www.jd.com/')
    next_page()
```



### 解决：'chromedriver' executable needs to be in PATH问题

1.  [下载地址](http://npm.taobao.org/mirrors/chromedriver/)

    下载chromedriver，**网址：http://npm.taobao.org/mirrors/chromedriver/
    （1）确定当前浏览器版本
    确定好Chrome浏览器版本号，浏览器右上角三个点-帮助-关于Google Chrome，就能看到当前版本号，我的是80.0.3987.149，确定好之后接下来我们要去找到对应的[chromedirver驱动](https://chromedriver.storage.googleapis.com/index.html?path=80.0.3987.106/)；
    （2）下载对应版本驱动chromedriver
    下载chromedriver后，解压，将chromedriver文件放到chrome目录：

    ```
    C:\Users\quent\AppData\Local\Google\Chrome\Application
    ```

    **单独测试时，可放到项目目录中，涉及到项目的相对路径就不行**

2.  测试

    ```
    from selenium import webdriver
    chrome_driver = "C:/Users/quent/AppData/Local/Google/Chrome/Application/chromedriver.exe"
    driver = webdriver.Chrome(executable_path=chrome_driver)
    driver.get(“https://www.baidu.com/”)
    ```

    

3.  