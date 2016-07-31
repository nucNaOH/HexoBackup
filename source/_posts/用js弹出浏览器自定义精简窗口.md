---
title: 用js弹出浏览器自定义精简窗口
date: 2016-07-30 23:28:30
categories: [JavaScript]
tags: [JavaScript, 浏览器]
---
有时候，由于某些需求，一些网页需要更大块儿的像素区域来展示更多更丰富的信息，这时可通过JavaScript对浏览器边框进行自定义“精简”，来达到这样的目的。
<!-- more -->

### 代码实现

我们可以调用如下的函数控制浏览器弹出自定义精简窗口。
``` JavaScript
// 定义新窗口相关的变量
var newWindow = null;
var newWindowName = "new_window";
var newWindowFeature = "resizable=yes, scrollbars=yes, left=200, top=100, width=600, height=400";

function popUpSimpleWindow(){
	// 判断该窗口是否已经打开
	if(newWindow == null || newWindow.closed) {
		// 打开上述自定义特性的窗口
		newWindow = window.open("http://nucNaOH.github.io", newWindowName, newWindowFeature);
	}else{
		newWindow.focus();
	}
}

popUpSimpleWindow();
```
效果如下图：
![精简窗口](http://oa6lwc3gp.bkt.clouddn.com/image/%E7%B2%BE%E7%AE%80%E6%B5%8F%E8%A7%88%E5%99%A8%E7%AA%97%E5%8F%A3.png)

### 原理详解

关键的代码如下：
``` JavaScript
newWindow = window.open(url, newWindowName, newWindowFeature);
```
该函数的有三个参数，分别为新窗口的url、新窗口的标识name(String)、新窗口的特性值feature(String，逗号分隔)，还返回该窗口对象的引用nenWindow，我们可以借此加一层判断，实现同时只可以有一个新窗口存在，如最上面的代码。

其中第三个参数可以自行选择设定。这里先普及一下浏览器页面上各元素的名称：
![浏览器介绍](http://oa6lwc3gp.bkt.clouddn.com/image/%E6%B5%8F%E8%A7%88%E5%99%A8%E9%A1%B5%E9%9D%A2%E8%AF%B4%E6%98%8E.gif)

参照上面的图，便可通过`window.open()`函数对新窗口的页面元素进行自定义。比如上面的`resizable=yes, scrollbars=yes`,还有`menubars,titlebars,location`等等。

这里支持4种风格的字符串配置风格：
>1. menubar=yes,toolbar=yes,scrollbars=no
>2. menubar=on,toolbar=on,scrollbars=off
>3. menubar=1,toolbar=1,scrollbars=0
>4. menubar,toolbar,scrollbars(写的有，不写的就没有)

更详细的参数说明请参考[JavaScript开发手册](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/open)

### 额外说明

1. 某些情况下，用户对浏览器的设置可能导致某些特性按用户的设定来，而非js里的设定；
2. 某些安全软件可能禁止了浏览器弹出新窗口；
3. 调用window.open()方法以后，远程 URL 不会被立即载入，载入过程是异步的。（实际加载这个URL的时间推迟到当前脚本块执行结束之后。窗口的创建和相关资源的加载异步地进行。）