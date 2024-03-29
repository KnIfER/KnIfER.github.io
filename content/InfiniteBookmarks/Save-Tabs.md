## chrome怎样在长页面中添加书签(标记)？

在浏览一个很长的页面时，如阅读某些文档时，怎样在页面中间位置添加书签，下次还能接着阅读？

[本文首发于知乎](https://www.zhihu.com/question/26936077/answer/3255947645)

两个回答里提及的“光线书签”已经挂了，chrome 里 404，全网也只找到一个需要关注公众号才能下载的网站。有点好奇它是怎么将滚动位置与书签挂钩的，将数值写入标题还是url？

保存滚动位置，**实际上有一个更加通用的需求：保存标签页。**发现如果关闭标签页，下次启动再打开，chrome大概是能记住滚动位置的，证明标签页的浏览状态被保存。

chrome 本身就有保存标签页的办法：右击固定标签页、新版本听说可以保存和恢复标签页分组。然而“固定标签页”并不能用于保存浏览数据，反而不如不固定，手动或自动恢复标签页（设置-启动时-继续浏览上次打开的标签页）。

  

理论上保存标签页能够将滚动位置、导航历史、sessionStorage都保存下来，以待恢复。然而chrome并未提供完全相应的接口。

我找了一些号称能保存标签页的扩展，不是难用、找不到入口，就是功能简单，无法真正保存标签页，比如那个onetab，实际只记录标签页地址，就把你所有页面都关闭了。

### 还得我出手

我闭收（开发不了）的“无限书签扩展”，其中的一个子功能，就可以临时保存一些网站地址。v2.7新增“保存会话数据”的右键菜单，新增：保存一部分会话数据的能力，右击恢复。

动图演示：

![](https://pic1.zhimg.com/50/v2-cee4f28f83c03dd7b5c2f2da34f37e1d_720w.gif?source=2c26e567)

动图解读：滚动页面至任意位置，然后打开无限书签，进入“重要页面”或“临时收藏”小页面，点击其中加号按钮以添加当前地址。右击新加入的图标，选“保存会话数据”，这样滚动位置就与sessionStorage 一起保存在小页面之中。可以右击选择“恢复”，也可以打开新的窗口。

按住ctrl再点加号，可以重复添加url，然后保存不同的滚动位置。

## sessionStorage 有什么用

有些网站会将一些界面状态，比如嵌套控件的滚动位置、瀑布流分页、翻页位置等等，恢复 sessionStorage 即可恢复这些状态。

需要注意的是有时需要刷新，恢复的 sessionStorage 才生效。