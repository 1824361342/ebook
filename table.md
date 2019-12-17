
# 使用网页浏览器显示表格

网页浏览器(Webviewer)除了可以显示现成的网页之外，我们还可以用来显示表格。

本文需要简单的html+javascript+css知识。

## 网页浏览器与html如何交互
在网页浏览器组件中，我们可以通过`设置网页浏览框.页面交换字符串为`块和`执行javascript`块来向html文件发送数据。

在html文件中使用javascript来设置页面交换字符串`window.AppInventor.setWebViewString("str")`， 或者设置页面标题`document.title = "str"`。这样就可以通过`页面浏览器.页面交换字符串`块或者`当前页标题`来获取返回的值。

在wxbit中内置了`执行javascipt`块，

![2019-05-20_135826](http://cdn.kevinkun.cn/xsj/2019-05-20_135826.png)

对于其他服务器没有这个内置块，可以自定义过程如下：

![2019-05-20_125200](http://cdn.kevinkun.cn/xsj/2019-05-20_125200.png)

## 准备html文件
新建一个html文件，在body中插入以下代码
```javascript
			function showTable(jsonData){				

				var data = JSON.parse(jsonData);
				var head = data[0];				

				var str = "<table'>";
				str += "<tr>";
				for(var j=0; j<head.length;j++){
					str += "<th>" + head[j] + "</th>";
				}
				str += "</tr>";
				
				
				for(var i=1; i<data.length;i++){
					str += "<tr>";
					for(var j=0; j<data[i].length;j++){
						str +=  "<td>" + data[i][j] + "</td>";
					}
					str += "</tr>";
				}
				str += "</table>";
		
				document.body.innerHTML="";	
				var table =document.createElement("div");
				table.innerHTML=str;
				document.body.appendChild(table);
			}
```
在`<head>`和`</head>`之间插入以下css片段，可以让表格显示的更加美观：
```css
<style type="text/css">
table {
    font-family: verdana,arial,sans-serif;
    font-size:11px;
    color:#333333;
    border-width: 1px;
    border-color: #666666;
    border-collapse: collapse;
	width:100%;
}
th {
    border-width: 1px;
    padding: 8px;
    border-style: solid;
    border-color: #666666;

    
}
td {
    border-width: 1px;
    padding: 8px;
    border-style: solid;
    border-color: #666666;
	text-align:center;
   
}

tr:nth-child(even){
	background:lightgreen;
}
</style>
```
将html文件另存为table.html文件，并上传到项目的素材中。

## 显示表格
在Screen1中添加一个按钮和一个网页浏览器。
首先,让网页浏览器打开素材中的table.html
![2019-05-20_140918](http://cdn.kevinkun.cn/xsj/2019-05-20_140918.png)

假设我们要用表格显示的数据如下：

姓名|性别| 年龄
---|---|---
张三 |男|23
李四| 女|34
王五| 男|45

我们就可以这样调用JS:

![2019-05-22_104502](http://cdn.kevinkun.cn/xsj/2019-05-22_104502.png)

这里有个关键点：
*组件设计界面，Screen1的右侧的组件属性最下面，有个`是否将列表转为JSON`,这个必须选中。*

![2019-05-22_104913](http://cdn.kevinkun.cn/xsj/2019-05-22_104913.png)

现在，就可以在手机伴侣中点击按钮，就看到如下效果：

![2019-05-21_130414](http://cdn.kevinkun.cn/xsj/2019-05-21_130414.png)

## 返回选中结果

怎么才能让AppInventor获取我们点中的某行某列呢？
只要在html中添加以下js代码：

```javascript
function tabClick(){
				var td = event.srcElement;
				var str = '{"row":"' + (td.parentElement.rowIndex+1) + '","col":"' + (td.cellIndex+1) + '","value":"' + td.innerHTML + '"}';
				//console.log(str);
				//window.AppInventor.setWebViewString(str);
				document.title = str; //将选中的行号和列号赋值为文档标题
			}
```
将showTable函数的第三行改为：
```javascript
var str = "<table onclick='tabClick();'>";
```
记得要把html文件重新上传到素材

在ai中添加一个计时器，计时间隔设为100
然后，配合计时器就可以获取到选中的行和列了

![2019-05-20_143417](http://cdn.kevinkun.cn/xsj/2019-05-20_143417.png)

点击表格，会返回行号、列号和单元格的值。

![2019-05-21_130450](http://cdn.kevinkun.cn/xsj/2019-05-21_130450.png)

这个返回值是个json格式，可以配合`Http客户端.解码JSON文本`和列表的`在键值列表...中查找`来取得行号、列号等。



相关下载：

[右键另存为table.html](http://cdn.kevinkun.cn/ai/20190526/pMUFQOFF05GC.html)

（完）

