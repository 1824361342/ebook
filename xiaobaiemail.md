# 小白接口发送邮件

## 准备工作

- 小白接口网站注册账号：[点我注册](http://open.yesapi.cn/?r=user/registration&from=wangsk789)
- 进入个人中心，记下你的接口域名和app_key
- 为简单起见，关闭“App.Email.Send”接口的签名设置。[点我查看方法](https://cdn.kevinkun.cn/ai/20200111/7T4STaqSTCNm.png)
- 配置邮箱服务。[点我查看方法](https://cdn.kevinkun.cn/ai/20200111/51wxsmz0A6yj.png)
- 了解邮件发送接口文档：http://hb5.api.okayapi.com/docs-api-App.Email.Send.html



## 组件设计界面

![mark](https://cdn.kevinkun.cn/ai/20200111/ouyjVAtW29ho.png)

主要组件：

1. 文本输入框，改名为收件人
2. 文本输入框，改名为主题
3. 文本输入框，改名为正文
4. 按钮，改名为添加附件
5. 标签，改名为附件名，文本设为空
6. 按钮，改名为发送邮件
7. HTTP客户端，用来负责与接口api通讯，解析服务器返回值
8. 文本选择框，用来选择附件
9. 文件管理器，用来将文件转为BASE64编码
10. 信息对话框，提示发送成功与否



## 逻辑设计界面

==黑科技：以下代码可以直接拖拽到wxbit逻辑设计界面==

1. 初始化几个全局变量，

![mark](https://cdn.kevinkun.cn/ai/20200111/k3Cs3Xo8yHVN.png)

![mark](https://cdn.kevinkun.cn/ai/20200111/ts6xQERPQ80y.png)

![mark](https://cdn.kevinkun.cn/ai/20200111/SsJfvjMtrE15.png)

2. 添加附件

   ![mark](https://cdn.kevinkun.cn/ai/20200111/U0WCxOGt2nrW.png)

   ![mark](https://cdn.kevinkun.cn/ai/20200111/Ssm1vucNjx0o.png)

3. 发送邮件函数

   参照接口文档，几个必选参数有app_key，address（收件人，可以用英文逗号分隔），title（邮件标题），content（邮件正文，可以是html格式）。附件attachments是可选参数，如果是图片，需要base64编码。

![mark](https://cdn.kevinkun.cn/ai/20200111/28t4ilRuyVKp.png)

使用==合并文本==来拼接字串，拼出网址和POST文本，注意其中的文本格式，这里的附加内容是base64文本，需要URL编码。如果需要添加抄送、密送等，查看文档看参数。

4. 发送邮件

   ![mark](https://cdn.kevinkun.cn/ai/20200111/pR2UC607wqTV.png)

如果没有附件（附件名.文本为空），就直接发送。如果有附件，就先将附件进行base64编码。

5. 编码完成在发送

![mark](https://cdn.kevinkun.cn/ai/20200111/VVegAUFBidjd.png)

6. 提示是否发送成功

![mark](https://cdn.kevinkun.cn/ai/20200111/lzkOHGHz04FP.png)

根据接口文档，返回是个json文本，其中的data.err_code如果为0说明发送成功。如果发送错误，查看是否是ak或地址写错，或者附件太大。

若附件太大，建议使用

![mark](https://cdn.kevinkun.cn/ai/20200111/ImQnXvo0akl2.png)

将图片缩小到800*800后再发送。