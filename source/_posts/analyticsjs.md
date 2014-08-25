title: google-analytics的使用: 解析页面引入代码
date: 2014-08-22 16:16:07
tags: 工具
---
## 代码整理和注释
    // 创建ga()方法, 加载analytics.js文件
    // a, m 作为形参，确保下面的执行不会修改外部的同名变量
    (function(win, doc, o, g, ga, a , m){
        
        win['GoogleAnalyticsObject'] = ga;      // 向外暴露出ga对象
        // 确保只执行一次analytics.js的插入
        win[ga] = win[ga] || function() {

            (win[ga].q = win[ga].q || []).push(arguments)},
            win[ga].l = 1 * new Date();         // 把时间格式转换成数字型
            
            // 动态加载analytics.js
            a = doc.createElement(o),
            m = doc.getElementsByTagName(o)[0]; // script
            a.async = 1;
            a.src = g;
            m.parentNode.insertBefore(a, m);
    })(window, document, 'script','//www.google-analytics.com/analytics.js','ga');

短短的代码, 还是蛮有货的，呵呵。   
## 压缩的代码

    (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)})(window,document,'script','//www.google-analytics.com/analytics.js','ga');

参考: [https://developers.google.com/analytics/devguides/collection/analyticsjs/advanced?hl=zh-TW](https://developers.google.com/analytics/devguides/collection/analyticsjs/advanced?hl=zh-TW)