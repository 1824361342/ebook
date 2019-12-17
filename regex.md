
# 规则表达式插件

## 下载地址

aix：[cn.kevinkun.RegEx.aix](http://cdn.kevinkun.cn/ai/20190526/iAgRVMXz2qyw.aix)

## 方法

![regex1](http://cdn.kevinkun.cn/xsj/regex1.png)

GetMatches方法可以返回符合条件的字符串列表

SplitWith方法可以使用规则表达式对字符串进行分割，并返回列表

![regex2](http://cdn.kevinkun.cn/xsj/regex2.png)

ReplaceFirst方法和ReplaceAll方法可以返回替换第一个或所有符合条件的子字符串后的新字符串

![regex4](http://cdn.kevinkun.cn/xsj/regex4.png)

IndexOf方法可以返回符合条件的第一个字串的位置

![regex3](http://cdn.kevinkun.cn/xsj/regex3.png)

IsMatch方法可以判断字符串是否符合规则表达式，返回真或假

IsNumber方法可以判断字符串是否为数字格式

IsEmail方法可以判断字符串是否为邮箱格式

IsStrongPassword方法可以判断字符串是否为强密码（至少8位，只好有1位大写和1位小写和1为数字）

IsEmail和IsStrongPassword可以用在用户注册、登录等情况

(完)
