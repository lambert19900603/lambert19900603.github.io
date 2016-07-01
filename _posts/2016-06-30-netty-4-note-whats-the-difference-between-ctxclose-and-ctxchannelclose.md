---
layout: post
title: "Netty 4 Note: what's the difference between ctx.close and ctx.channel.close?"
description: ""
date: 2016-06-30
time: 16:45:18
author: Lambert Bao
header_img: img/bg-1.jpg
category: 
tags: [Netty]

---

> 原文转自stackoverflow：
> [http://stackoverflow.com/questions/21240981/in-netty-4-whats-the-difference-between-ctx-close-and-ctx-channel-close](http://stackoverflow.com/questions/21240981/in-netty-4-whats-the-difference-between-ctx-close-and-ctx-channel-close)

假设pipeline中有三个handler，它们均包含`close()`方法，并且在该方法中调用了`ctx.close()`。

	{% highlight java %}
	ChannelPipeline p = ...;
	p.addLast("A", new SomeHandler());
	p.addLast("B", new SomeHandler());
	p.addLast("C", new SomeHandler());
	...
	
	public class SomeHandler extends ChannelInboundHandlerAdapter {
	    @Override
	    public void close(ChannelHandlerContext ctx, ChannelPromise promise) {
	        ctx.close(promise);
	    }
	}
	{% endhighlight %}

- `Channel.close()`将触发`C.close()`，`B.close()`，`A.close()`，然后关闭channel。
- `ChannelPipeline.context("C").close()`将触发`B.close()`，`A.close()`，然后关闭channel。
- `ChannelPipeline.context("B").close()`将触发`A.close()`，然后关闭channel。
- `ChannelPipeline.context("A").close()`将关闭channel，不会触发其他handler。

总结使用`Channel.close()`和`ChannelHandlerContext.close()`规则如下：
- 如果你想在handler中关闭channel，请调用`ctx.close()`。
- 如果你尝试在handler外关闭channel（比如你先在一个非I/O的后台线程中关闭连接），请调用`Channel.close()`。