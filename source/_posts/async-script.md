title: 比较JS文件加载：async和DOM Script
---
async与script动态加载都能使文件异步加载，本文叙述它们对页面渲染和load加载的影响方面。  
<!-- more -->
目前我用demo.js作为执行文件操作.代码：
    
    var now = function() { return +(new Date()); }
    var t_s = now();
    while(now() - t_s < 2000) {  }

用sleep.php作为请求文件操作。代码：

    <?php
        sleep(3);
        echo 'var bb';
    ?>
## 1. 一般script标签加载
    <script src="demo.js"></script>
    <script src="sleep.php"></script>

在浏览器加载情况: **图1-1. 下载阻塞DomReady** **图1-2. 执行阻塞DomReady**
![](http://qnimg.qiniudn.com/140720/1-DOMReady.png)**图1-1. 下载阻塞DomReady**

![](http://qnimg.qiniudn.com/140720/2-DOMReady.png)  **图1-2. 执行阻塞DomReady**
## 2. async属性
async是html5中新增的属性，它的作用是能够异步下载脚本文件，不阻塞DOMReady。  
每一个async属性的脚本都在它下载结束之后立刻执行，同时会在window的load事件之前执行。所以就有可能出现脚本执行顺序被打乱的情况   
支持async浏览器: Firefox 3.6+, IE 10+, Chrome 2+, Safari 5+, iOS 5+, Android 3+

    <script src="demo.js" async></script>
    <script src="sleep.php" async></script>   
在浏览器中加载的情况：
![](http://qnimg.qiniudn.com/140720/1-async.png)**图2-1 异步下载 不阻塞DomReady 阻塞load事件** 

![](http://qnimg.qiniudn.com/140720/2-async.png)**图2-2 执行阻塞load事件**

![](http://qnimg.qiniudn.com/140720/3-ie-async.png)**图2-3 IE9不支持async属性下载阻塞DomReady**
## 3. DOM Script动态加载
文档对象模型（DOM）允许您使用 JavaScript 动态创建 HTML 的几乎全部文档内容。
script元素与页面其他元素一样，可以非常容易地通过标准 DOM 函数创建：

    var loadScript = function(url) {
        var s = document.createElement('script');
        s.type = 'text/javascript';
        s.async = 'true';
        s.src = url;
        document.getElementsByTagName('head')[0].appendChild(s);    
    }
    // 加载js文件脚本
    loadScript('sleep.php');
    loadScript('demo.js');
在浏览器中加载的情况：
![](http://qnimg.qiniudn.com/140720/1-script.png)**图3-1 下载阻塞load事件**

![](http://qnimg.qiniudn.com/140720/2-script.png)**图3-2 执行阻塞load事件**

![](http://qnimg.qiniudn.com/140720/3-ie-script.png)**图3-3 IE9不阻塞load事件**
## 小结
async和script动态加载在现代浏览器中加载的情况是一致的。前者使用简单，后在兼容性方面更好。  
异步加载文件还有很多方法，ajax(会受到同源限制)、iFrame、img...

参考链接：   
[http://ie.microsoft.com/TestDrive/Performance/AsyncScripts/Default.html](http://ie.microsoft.com/TestDrive/Performance/AsyncScripts/Default.html)  
[http://ued.ctrip.com/blog/?p=3121](http://ued.ctrip.com/blog/?p=3121)  
[http://blog.jobbole.com/47304/](http://blog.jobbole.com/47304/)    
[http://www.infoq.com/cn/articles/browser-resource-loading-optimization](http://www.infoq.com/cn/articles/browser-resource-loading-optimization)





