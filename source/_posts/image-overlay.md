title: 为图片添加半透明遮罩效果
date: 2014-09-04 07:22:25
tags: css, 工作经验
---
平时为图片添加半透明遮罩效果，我的做法如下： 
利用标签i实现背景半透明遮罩
```html
<p class="opacity-black-position"><a href="#"><img src="images/4601.jpg" alt=""><i></i></a></p>
```
为html结构添加如下css样式：
```css
/* 利用标签i实现背景半透明遮罩, 兼容性不好 */
.opacity-black-position { width: 460px; height: 460px; position: relative; }
.opacity-black-position i { 
    position: absolute; top: 0; right: 0; bottom: 0; left: 0; 
    background-color: rgba(0, 0, 0, 0); 
    transition: background-color .5s;  
}
.opacity-black-position a:hover i { background-color: rgba(0, 0, 0, .6); }
```
## 利用opacity简单实现
昨天看到京东商品图片上的半透明黑色遮罩，是这样实现的。 

让父容器a半透明
```html
<p class="opacity-black"><a href="#"><img src="images/4601.jpg" alt=""></a></p>
```
为html结构添加如下css样式:
```css
.opacity-black { width: 460px; height: 460px; background-color: #000; }
.opacity-black a { transition: opacity .5s; opacity: 1; }
.opacity-black a:hover { opacity: 0.4; }
```
虽然效果实现了，但是原理不是很清楚。如果你知道，还请不吝赐教。

**狠狠滴点这里(演示):** [http://codepen.io/mackxu/pen/mJtvh](http://codepen.io/mackxu/pen/mJtvh)
