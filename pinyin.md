# 如何让中文按照拼音排序



我们现在有个列表

![mark](https://cdn.kevinkun.cn/ai/20200113/btaD3WDj0soS.png)

想让他按照汉语拼音顺序排序，使用内置块排序如下：

![mark](https://cdn.kevinkun.cn/ai/20200113/X43hCujyrMx8.png)

返回结果是：["陈八", "赵六", "田七", "王五", "李四", "张三"]

这个并不是我们想要的结果。



## 准备工作

想让列表按照拼音排序，首先要把汉字转成拼音，最简单的方法就是查字典。

[点我下载字典文件](https://cdn.kevinkun.cn/ai/20200113/Pp41hLGno4hm.json)，改名为pinyins.json,上传到项目的素材库。

在项目中放入一个按钮、一个标签、一个文件管理器、一个HTTP客户端



## 逻辑设计

### 将字典导入项目

![mark](https://cdn.kevinkun.cn/ai/20200114/bQaFacgKP5TQ.png)

![mark](https://cdn.kevinkun.cn/ai/20200113/DqpGwUn1tiBU.png)

![mark](https://cdn.kevinkun.cn/ai/20200114/mRH6c2gts6er.png)

字典文件可以在电脑上用记事本打开查看内容，是个这样的JSON格式的文本：

![mark](https://cdn.kevinkun.cn/ai/20200113/KYjq9CinGLle.png)

使用解码JSON文本，可以将他转换为键值对列表

### 查字典将汉字转为拼音

![mark](https://cdn.kevinkun.cn/ai/20200114/1KuguC0YTpBD.png)

查看字典文件内容可以发现，有些字是多音字，这里为了简便，我们只取第一个读音。

### 将一个字串（多个汉字或者字母数字）转为拼音

![mark](https://cdn.kevinkun.cn/ai/20200113/D9edU0lUaHEd.png)

![mark](https://cdn.kevinkun.cn/ai/20200114/c6TjeAV3Xu8d.png)

依次读取字串中的每个字符，如果是数字或者字母就原样输出，否则就转为拼音。

### 自定义排序方式

使用wxibt最新的`排序列表` 自定义排序方式

![mark](https://cdn.kevinkun.cn/ai/20200113/IPimdf4rLCn1.png)

### 现在可以按照拼音排序了

![mark](https://cdn.kevinkun.cn/ai/20200113/lOLTfeEjPx3n.png)

输出为 ["陈八", "李四", "田七", "王五", "赵六", "张三"]，正是我们想要的。

但是这样排序效率有点低（主要是因为频繁查字典），不要用它排序很长的列表。