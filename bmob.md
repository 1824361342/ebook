
# 比目微数据库扩展

内置的网络微数据库，服务器是国外公用服务器，速度慢，不安全。

比目微数据库可以代替内置的网络微数据库，但是更高效，更安全。

## 更新记录

- v2 修复了返回值全部为文本的bug, 更名为BmobDB。自带默认appid，apikey和tablename，可以不用设置就直接使用（仅做测试之用，默认key随时可能失效）。 
- v1 新发布

## 下载链接

- v2：[cn.kevinkun.BmobDB.v2.aix](http://cdn.kevinkun.cn/ai/20190626/KM4VHMwA3M9o.aix)
- v1：[cn.kevinkun.Bmob.v1.aix](http://cdn.kevinkun.cn/ai/20190625/qtAwqKAA84rL.aix)

## 准备工作

1. 注册比目账号 http://www.bmob.cn;
2. 进入“我的控制台”，创建应用，进入应用，添加表，记住表名;
3. 进入设置，记住 Application Id, Rest Api Key;

## 使用方法

跟内置的网络微数据库功能基本相同：



![mark](http://cdn.kevinkun.cn/ai/20190625/phwylk8durbc.png?imageslim)



~~注意：有点不同的是，保存数字、逻辑值、列表时，都会保存为文本格式。获取数据时，返回值也是个文本。~~

~~所以如果想保存列表的话，在组件设计界面，Screen1组件属性最下面，有个`是否将列表转为JSON`,这个必须选中。然后获取返回值后，可以使用`Http客户端.解码json文本`，变成列表格式。~~

~~![2019-05-22_104913](http://cdn.kevinkun.cn/xsj/2019-05-22_104913.png)~~

(完)


