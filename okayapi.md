
# 小白接口扩展

小白接口，免费，免开发，直接可用的云端数据接口



## 更新:

小白官网网址已经改为http://www.yesapi.cn



## 下载链接

- [cn.kevinkun.OkayApi.aix](http://cdn.kevinkun.cn/ai/20190526/QVsfl6eBHatl.aix)
- [demo aia](http://cdn.kevinkun.cn/ai/20190526/mdT8UuSpMBJu.aia)



## 准备工作

1. 注册小白账号 <a href="http://www.okayapi.com/?f=wangsk789">http://www.okayapi.com</a>
2. 进入&quot;我的套餐&quot;，记下接口域名、app_key、app_secret。
3. 进入“我的数据库”，创建一个新模型(自定义数据库)，记下数据库名和各字段名。



## 属性

![2018-11-07_092119](http://cdn.kevinkun.cn/xsj/2018-11-07_092119.png)

设置接口域名

![2018-11-07_092106](http://cdn.kevinkun.cn/xsj/2018-11-07_092106.png)

设置appKey

![2018-11-07_092111](http://cdn.kevinkun.cn/xsj/2018-11-07_092111.png)

设置appSecret

![2018-11-07_092125](http://cdn.kevinkun.cn/xsj/2018-11-07_092125.png)

设置是否显示隐藏错误信息。默认是否（不隐藏）。



## 方法

以下方法的接口参数格式，可以参照这里的接口文档 <a href="http://api.okayapi.com/docs.php">http://api.okayapi.com/docs.php</a>自定义数据模型部分

![2018-11-07_092315](http://cdn.kevinkun.cn/xsj/2018-11-07_092315.png)

### 查询数据库

table：数据库名

fields：字段名，多个字段用半角逗号隔开。空字串表示全部字段

where：查询条件，形式如` ["nianling",">","35"]` ，空字串表示全部记录 

第一个位置表示字段名称（字段必须先存在）, 

第二个位置表示判断>符号（可以是：>、>=、<、<=、=、<>、LIKE、NLIKE、IN、NIN、BETWEEN、NBETWEEN）, 

第三个位置表示判断值。

如果是多个条件，用半角逗号隔开，例如： ["id",">",9],["id","<=",10] 。

几个例子：

查询id=7，id=70，id=700这三个ID，可以写["id","IN",[7,70,700]]。

查询某个月1号到30号添加的数据，可以写["add_time","BETWEEN",['2019-06-01 00:00:00', '2019-06-30 23:59:59']]

logic: 如果where为多个条件时，logic可以设为and或者or

order：排序字段，形式如 `gongzi DESC` ,空字串表示按记录添加时间排序

limit: 返回记录的数量。最大2500，空字串表示默认500.

![2018-11-07_092158](http://cdn.kevinkun.cn/xsj/2018-11-07_092158.png)

### 插入记录

table：数据库名

datas：插入的数据，需要json格式。形式如`[{"username":"lee","score":80}]`。如果是多条记录，用半角逗号隔开。注意必须有方括号

![2018-11-07_092217](http://cdn.kevinkun.cn/xsj/2018-11-07_092217.png)

### 更新记录（文本方式）

data：要修改的数据，需要json格式。形式如`{"username":"lee","score":80}`。官方文档中不能有方括号，这里可有可无。

其他插口说明见以上方法

![2018-11-07_092225](http://cdn.kevinkun.cn/xsj/2018-11-07_092225.png)

### 更新记录（批量四则运算）

field：要更新的字段

op：取值范围add/sub/mul/div,即加/减/乘/除

number: 待运算的数字，例如加多少，减多少，乘多少，除多少。必须为合法的数字，可以是小数

field=gongzi&op=add&number=500 就是gongzi=gongzi+500

![2018-11-07_092236](http://cdn.kevinkun.cn/xsj/2018-11-07_092236.png)

### 删除记录

插口说明见以上方法

![20181118194335027](http://cdn.kevinkun.cn/xsj/20181118194335027.jpg)

### 将csv格式转化为json格式

比如`shuxue,yuwen,yingyu\n78,89,78\n90,95,94`
转化为
`[{"shuxue":" 78","yuwen":"89","yingyu":"78"},{"shuxue":" 90","yuwen":"95","yingyu":"94"}]`

## 事件

![20181118194222724](http://cdn.kevinkun.cn/xsj/20181118194222724.jpg)

### 查询结束事件

recordCount:符合条件的记录条数

recordList:查询结果，列表格式，第一行为字段名，第二行开始是数据

![2018-11-07_092431](http://cdn.kevinkun.cn/xsj/2018-11-07_092431.png)

### 数据变化事件

添加、修改、删除后引发此事件。

affectedRowNum: 收到影响的记录条数

action：引发此事件的方法：insert/update/delete 

（完）

