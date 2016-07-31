---
title: Ajax用JQuery实现的一种个人常用写法
date: 2016-07-30 21:23:21
categories: [JavaScript]
tags: [Ajax, JQuery, JavaScript]
---
Ajax，即Asynchronous JavaScript and XML，翻译过来就是：异步的JavaScript与XML技术。个人的理解是：一种用JS在浏览器上执行的想服务器发送请求以获取相应数据技术，使用它可以很方便地在不更新页面的前提下请求、获取、处理、显示数据。

<!-- more -->

 这种技术在浏览器上应用非常广泛，这里仅记录几种我个人用Ajax时常用的方便调试的写法。

## JQuery写法

### 个人自用写法

``` JavaScript
$.ajax({
    url: "http://nucNaOH.github.io/",
    type: "POST",
    timeout: 5000,
    async: false,         // default is true
    data: {
        text: text
    },
    dataType: "json",       // xml,json,jsonp,script,html,text.
    // 一般从数据库查找出来的结果，返回都是json格式。页面用html
    beforeSend: function(jqXHR) {
        // console.log('beforeSend:'+text);
    },
    success: function(data) {
        // console.log('success'+data);
    },
    error: function() {
        // console.log(jqXHR);
        // 该函数的三个参数：
        // jqXHR jqXHR, String statusText, String errorThrown
    },
    complete : function(jqXHR, statusText, settings) {
        // 无论success、error都会执行，且在success、error之后
    }
});
```
### 连贯写法：
``` JavaScript
var jqxhr = $.ajax( "example.php" )
  .done(function() {
    $( this ).addClass( "done" );
    // alert( "success" );
  })
  .fail(function() {
    alert( "error" );
  })
  .always(function() {
    alert( "complete" );
  });
```

## 原生js写法

原生的JavaScript实现ajax技术的写法：
### 精简版
``` JavaScript
function reqListener() {
    console.log(this.responseText);
}

var oReq = new XMLHttpRequest();
oReq.onload = reqListener;
oReq.open('get', 'some.php', true);
oReq.send();
```

### 多事件监听版
``` JavaScript
var req = new XMLHttpRequest();

req.addEventListener("progress", updateProgress, false);
req.addEventListener("load", transferComplete, false);
req.addEventListener("error", transferFailed, false);
req.addEventListener("abort", transferCanceled, false);

req.open();

// 传输进度监听 (下载)
function updateProgress(evt) {
  if (evt.lengthComputable) {
    var percentComplete = evt.loaded / evt.total;

  } else {
    // 总长度没设置时无法监听进度
  }
}
```

## 相关文章
- [Using XMLHttpRequest](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest)
- [jQuery.ajax()](http://api.jquery.com/jQuery.ajax/)
- [XMLHttpRequest](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest)