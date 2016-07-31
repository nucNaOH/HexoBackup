---
title: js小技巧之----获取窗口resize完成之后的事件
date: 2016-07-31 00:46:31
categories: [JavaScript]
tags: [JavaScript, Event]
---

用js可以方便地获取浏览器窗口`onResize`事件，当窗口在被resize的时候，该事件会不断被触发。然而，想要获取窗口resize完成之后的事件(`onResizeCompleted`)却比较麻烦。

<!-- more -->

## 获取`onResize`事件

### js原生代码

如下：
``` JavaScript
window.addEventListener('resize', function() {
	console.log(window.innerWidth + ' ' + window.innerHeight);
});
```

### JQuery代码

如下：
``` JavaScript
$(window).on('resize', function() {
	console.log($(window).width() + ' ' + $(window).height());
});
```
上面的代码，可以使浏览器在resize的时候在控制台console实时输出当前页面的长、宽像素。这里就不贴图了，可以看到随着鼠标对浏览器窗口的拖动(onResize)时，console里有很多的数据在实时输出。也就是说，上面的函数在resize的时候执行了很多次！

那么问题来了：如果我想只想监听浏览器窗口resize结束的事件该怎么做呢？也就是说，如果我只想让一个函数在浏览器窗口resize结束之后只执行一次，而不是一直执行，该怎么做呢？

## 获取`onResizeCompleted`事件

### js原生代码

``` JavaScript
var resizeTimer;
window.addEventListener('resize', function() {
	clearTimeout(resizeTimer);
	resizeTimer = setTimeout(function() {
		// 此函数会在resize结束的时候执行
		console.log('onResizeCompleted');
	}, 250);
});
```

### JQuery代码

``` JavaScript
var resizeTimer;
$(window).on('resize', function(e) {
  clearTimeout(resizeTimer);
  resizeTimer = setTimeout(function() {
    // 此函数在resize结束的时候执行
    console.log('onResizeCompleted');
  }, 250);
});
```

这里利用setTimeout()函数配合对应的clearTimeout()函数不断被执行，实现了简单的计时器Timer，当resize事件触发后停下来的250ms时间后，执行内部的匿名函数，模拟实现对`onResizeCompleted`事件的监听。当然，这里的250ms可以根据实际的需求进行自己的设定，不过已经符合大部分的情况了，我在noVNC里也见到过同样的设定。

## 总结

这种小技巧，可能会在处理别的类似的事件的时候会有用，有待验证。