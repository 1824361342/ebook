# SocketIO客户端扩展



SocketIO客户端可以用来开发实时网络聊天，实时网络游戏等…



## 方法与事件

### Login 连接到服务器

serverUrl:服务器地址（可以自己部署服务器，见后面教程）

userName：用户名。 若服务器上已有同名用户，会引发“GotError”事件，原因：duplicate username

连接成功后，会引发Logedin事件，其他在线用户会收到OtherLogedin事件，返回登录人的姓名和当前在线人数

![mark](http://cdn.kevinkun.cn/ai/20200105/xMVVyIGXUfKy.png?imageslim)



### Logout 断开服务器连接

主动断开与服务器连接。用户会收到Logedout事件，其他用户会收到“OtherLogedout”事件，返回离开人的名称和当前在线人数。

因网络不好等原因与服务器失去联系，也会收到此事件。

![mark](http://cdn.kevinkun.cn/ai/20200105/ATXwt9nl4aui.png?imageslim)

### JoinOrCreateRoom 加入或创建房间

若服务器没有此房间，将创建房间并加入，并设置房间最大容纳人数maxUser。 

若房间已经存在，将加入房间，maxUser参数无效。

若房间人员已满，将收到“GotError”错误事件：room full（房间已满）

若成功加入，会收到JoinedRoom事件，其他人收到“OtherJoinedRoom”事件，同时返回新人名称、房间名称、当前房间人数、人员列表

一人可以同时加入多个房间。



![mark](http://cdn.kevinkun.cn/ai/20200105/aXzuVm82GUR7.png?imageslim)

### LeaveRoom 离开房间

主动离开某个房间。 其他人会收到“OtherLeftRoom”事件，并返回离开人名称、房间名称、当前房间人数、人员列表。

若某人断开服务器（主动或非主动），他之前所在房间的其他人也会收到“OtherLeftRoom”事件

![mark](http://cdn.kevinkun.cn/ai/20200105/A4qd5Jg8sxv3.png?imageslim)



### SendPrivateMessage 发送私人信息

给某用户发送私信，只有他能收到。

若该用户不存在，将收到“GotError”事件，原因：no such user

![mark](http://cdn.kevinkun.cn/ai/20191228/0L9tYsvc56Fn.png?imageslim)

### SendPublicMessage 发送公共消息

所有连接到服务器的用户（包括发送者）都能收到此消息

![mark](http://cdn.kevinkun.cn/ai/20191228/fJTqzYcM0LL3.png?imageslim)

### SendRoomMessage 发送房间消息

所有在该房间的用户（包括发送者）都能收到此消息

必须存在该房间，并且发送者必须在该房间内才能发送消息。 否则将收到“GotError”事件，原因：no such room or not in it

![mark](http://cdn.kevinkun.cn/ai/20191228/za2NG1QK3Vxh.png?imageslim)

### GotError 发生错误

出错时发生该事件, 原因有“not able to connect server”, “duplicate username”, "room full", "already in room", "no such room or not in it", "no such user"等等.

![mark](http://cdn.kevinkun.cn/ai/20191228/pj2O2t3QRJOt.png?imageslim)



## 如何自己部署服务器

服务器源码已经上传到github。 [点这里](https://github.com/wangsk789/kevinkun-chat) 获取源码，你可以将它部署到支持nodejs的服务器上。

我已经将服务器部署到[heroku](http://www.heroku.com), 你可以直接免费使用这个服务器地址: https://kevinkun-chat.herokuapp.com



## 下载链接

[cn.kevinkun.SocketIO.v2.aix](http://cdn.kevinkun.cn/ai/20200105/JLL1f8OPlsGM1.aix)

若无法下载看左边找联系方式



## 最后的话

Socket.io的功能远不止如此，如果你有其他的需求，请直接联系我。

