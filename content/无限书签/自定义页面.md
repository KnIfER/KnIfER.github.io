“自定义页面”(custom pagelet) 允许用户输入html与一段javascript代码，实现自定义的功能，比如实现嵌入百度高级搜索的引导页、简易计算器、图像文件转base64、字符串加密解密等等。

这里收录一些自用的小页面代码：[KnIfER/Infinite-Pagelets](https://github.com/KnIfER/Infinite-Pagelets)



# 一、无限书签扩展的“自定义页面”

这时候介绍一下[无限书签扩展](https://www.baidu.com/s?ie=utf-8&wd=%E6%97%A0%E9%99%90%E4%B9%A6%E7%AD%BE%E6%89%A9%E5%B1%95)的“自定义页面”功能。

[高赞回答](https://www.zhihu.com/question/28531079/answer/41508740)：“地址栏就是个计算器，非常方便，常用。”可惜，google的网址无法访问，而且不能切换搜索引擎，明显是故意的！

![](https://pic2.zhimg.com/v2-024721bf7b5916730afae219f5d7d2b9_b.jpg)

地址栏就是个计算器

### 没关系我会出手

“自定义页面”本来用于自定义搜索引擎，可以将“百度高级搜索”的页面写进去，记忆各个搜索字段（已内置模板）。

也可以运行其他的脚本逻辑，比如计算器，让机器人写：

![](https://pic1.zhimg.com/v2-4e1a0e55912543e70cb3acb2e4e39e68_b.jpg)


改后脚本在后面。使用方法：复制后，扩展里新建自定义页面，右击标签栏选“编辑源代码”，粘贴后回车保存：

![](https://pic4.zhimg.com/v2-214c668aaf367da8c581ee178d2a5e1b_b.jpg)


输入源代码

  

![](https://pic2.zhimg.com/v2-48d5fffb3c0e863e69d861671dc632b9_b.jpg)

指数运算不可以

  
指数运算不可以。不用回车就能预览结果。

```text
<body>
  <textarea id="input" rows="4" cols="50"></textarea>
  <button id="button">Execute</button>
  <div id="output"></div>
</body>
<script>
	// “自定义页面”仅有一个代码块可以执行，执行方式为eval
	((bg)=>{
		var d = bg.view.s; // bg 是桥梁，view 是子页面视图，s是shadowDom
		d.getElementById('button').onclick = execute;
		var input = d.getElementById('input');
		var output = d.getElementById('output');
		var timer;
		input.addEventListener('input', function() {
			clearTimeout(timer);
			timer = setTimeout(()=>{
				execute()
			}, 200);
		});
		function execute() {
			try {
				var result = eval(input.value);
				output.innerHTML = `<p>Result: ${result}</p>`;
			} catch (error) {
				output.innerHTML = `<p>Error: ${error.message}</p>`;
			}
		}
	})(_bg());
</script>
</html>
		
```

很简单。无限扩展下去，可以加一些诸如繁简转换，加密解密之类的小按钮。

---

# 二、【小工具】用【无限书签扩展】在任意markdown编辑器网站中嵌入base64图片

刷zhihu的时候得知markdown的图片url里可以粘贴base64，这样就不用图床了：

```text
![image](base64)
```

有网友就根据这个原理，用electron造了个应用，打包出来两个70+MB的软件包，啧啧，g站的免费存储迟早要被你们造完……

其实这么简单的逻辑，直接发布一个html就行了，js直接写在里面，都不用分文件（你们**是不是不会）？**

而无限书签扩展提供了一种更加优雅的方式：可以将这种小工具写在扩展（弹窗）的小页面里面。默认的小页面是书签（性能一流）。自定义小页面可以写html+一段简单的js代码。

这么简单的逻辑还需自己写？还不问问机器人：

![](https://picx.zhimg.com/v2-1386c2f0cc0fe7882fe639540e9a5974_720w.jpg?source=d16d100b)


图片中是chatglm的回答，竟然能跑，功能完全就有了。据说隔壁的通义千问也不错，各种百宝箱，就是每次重启要重新登陆，不太方便。

然后开始优化，比如可以选择让他输出 markdown 格式还是普通的 html 格式，是否开启自动转换等等。

  

### 成品：

代码如下，可保存为html后在浏览器中打开，也可装入无限书签的小页面。

如何自定义小页面见我之前的文章。

![](https://picx.zhimg.com/v2-43cc692bf4f4a62c7f5786aaa69ee8d6_720w.jpg?source=d16d100b)


  
### 演示:

![](https://pic1.zhimg.com/v2-2695af5b9539c12b5bc7abbfea23b8e2.jpg?source=382ee89a)


视频解说：

预先写好小页面，我用书签栏上的小书签打开【无限书签扩展】，然后点击“选择文件”，打开想要嵌入的本地文件，由于预先勾选了“预览图像”，可以在下方预览选好的文件。由于预先设置好“自动转换”与“显示文本”，小页面自动开始将图像编码为base64格式，显示结果文本，并尝试自动复制到剪贴板，若复制成功底部有文字提示。

默认的封装格式是markdown，于是关闭扩展后，可粘贴到一些在线的markdown编辑器中。

效果一般，因为有的markdown编辑器不支持base64，或内容过长不予显示，有的一直换行导致可读性降低。

***

### 浅说js里复制文本怎么写

转换base64后，需要复制到剪贴板。恰好方才刷到一篇介绍许多js技巧的好文：

原来 javascript 里复制文本这么简单，一行三个词语就搞定了，我以前是这样复制的：

![](https://picx.zhimg.com/v2-cc85e6e5ea5ea8502d01a001194c1660_720w.jpg?source=d16d100b)


真正变成一行：navigator.clipboard.writeText(text)

。而chatglm是用的方式更原始（需要创建元素后才执行 execCommand）。

不过有时 navigator.clipboard 不存在，有时复制会失败，所以本例三个方法我都用了……