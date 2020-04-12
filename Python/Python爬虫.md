# Python爬虫

## 数据对比需求



1.  iGS产品和Garmin产品的FIT文件记录的数据差异；
2.  iGS的FIT文件差异：FIT文件、Strava及重新计算后的数据差异；
3.  Garmin的FIT文件差异：FIT文件、Strava、Garmin Connect的数据差异；



## 模拟chrome登陆



### cookie获取

![123](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/09/20200409101325.gif)

### 查找对应字段

![12](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/09/20200409095631.gif)

#### 

### 使用八爪鱼采集strava数据

基本流程：

1.  登陆strava，进入活动页面；
2.  采集所有的线路数据的概要信息；
3.  保存概要信息；
4.  循环：将概要信息中的数据链接打开，获得该活动详细信息后，更新线路的概要信息和详细信息，并自动下载对应的fit文件；


