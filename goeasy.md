
# Goeasy实现实时网络聊天室
## 前期准备

本教程使用了GoEasy的网络消息实时推送技术。
1. 注册账号。 GoEasy官网（https://goeasy.io）
2. 登录到GoEasy的后台管理系统，创建您自己应用app.
3. 应用创建好之后系统会自动为您生成appkey。有两个，一个是只能接受消息，一个是既可以发送，也可以接收消息。
4. 免费版本有1年的试用期，可以推送100000条消息，对于学习试验应该是足够了


## 组件设计界面
![4b5887fe9925bc313ebd54ef52df8db1ca137016](http://cdn.kevinkun.cn/xsj/4b5887fe9925bc313ebd54ef52df8db1ca137016.jpg)



1. 标签：聊天显示区。文本设为空，其他属性默认
2. web浏览器。可见性设为否，其他属性默认
3. 文本框：发送人ID 文本设为空，其他属性默认
4. 文本框：发送内容 文本设为空，其他属性默认
5. 按钮：发送按钮
6. 计时器：计时间隔设为50，其他属性默认
7. web客户端。属性都是默认

## 准备素材
将以下代码保存为goeasy.html，并上传到素材库：

```html
<!doctype html>
<html lang="en">
<head>
<meta charset="UTF-8">
<script type="text/javascript" src="https://cdn-hangzhou.goeasy.io/goeasy.js"></script>

</head>
<body>

</body>
<script type="text/javascript">
	var goEasy = new GoEasy({
		appkey: 'BC-7002587937f4419484a78fe674139818' //这里替换为自己的appkey
        
	});
	goEasy.subscribe({
		channel: "CH1",
		onMessage: function(message){
			window.AppInventor.setWebViewString(message.content);
		}
	});
</script>
</html>
```

## 实现的思路：
1. 使用web浏览器访问goeasy.html文件，订阅某个频道(这里是CH1)。只要这个频道下的数据有变化，系统就自动将变化的内容写给web浏览器的页面交换字串。
2. 使用web客户端来发布消息到CH1频道。这样，只要订阅了这个频道的人，都可以收到此消息。


## 逻辑设计界面
![2018-11-22_121312](http://cdn.kevinkun.cn/xsj/2018-11-22_121312.png)
1. 定义一个变量叫频道。这个变量的值可以修改，但必须与goeasy.html中的channel值相同
2. 定义一个变量KEY。因为是聊天程序，使用的是超级key（可发可收）这里要替换为自己的key
3. 定义个变量开发中。（注意:若要把本程序打包apk，必须先把这个变量设为假。若在手机伴侣中测试，设为真）
4. 给用户一个随机ID
5. 不用解释了
6. web浏览器若要使用素材库中的文件作为网络地址，在开发时和打包时使用不同的路径，需要根据情况修改开发中的值，见第3条。
7. 让web浏览器访问这个goeasy.html文件，就是订阅了CH1频道。
8. 若两个文本框都不为空
9. 这个网址在goeasy创建的应用后台管理里有。
10. 把消息发送出去。post文本的组成：必须有三个参数：appkey、channel、content。content需要使用URI编码
11. 不用解释
12. 让计时器不停的去问web浏览器是否收到消息。若页面交换字串不为空，表明web浏览器接收到了新消息。
13. 把新消息显示出来。
14. 把页面交换字串设为空，方便下次访问

