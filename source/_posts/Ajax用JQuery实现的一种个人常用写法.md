---
title: Ajax用JQuery实现的一种个人常用写法
date: 2016-07-30 21:23:21
categories: [JavaScript]
tags: [Ajax, JQuery, JavaScript]
---
Ajax，即Asynchronous JavaScript and XML，翻译过来就是：异步的JavaScript与XML技术。个人的理解是：一种用JS在浏览器上执行的想服务器发送请求以获取相应数据技术，使用它可以很方便地在不更新页面的前提下请求、获取、处理、显示数据。
<!-- more -->
##### 这种技术在浏览器上应用非常广泛，这里仅记录一种我个人用JQuery框架时的Ajax常用写法.
``` JavaScript
$.ajax({
    url: "http://localhost/",
    type: "POST",
    timeout: 5000,
    async: false,         // default is true
    data: {
        text: text
    },
    dataType: "json",       // xml,json,jsonp,script,html,text.
    //一般从数据库查找出来的结果，返回都是json格式。页面用html
    beforeSend: function(jqXHR) {
        // console.log();
    },
    success: function(data) {
        // console.log(data);
    },
    error: function() {
        // 该函数的三个参数：
        // jqXHR jqXHR, String textStatus, String errorThrown
    },
    complete : function(event, request, settings) {
        // 无论success、error都会执行，且在success、error之后
    }
});
```