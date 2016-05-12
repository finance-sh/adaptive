# adaptive
H5端自适应框架
使用方便，设计图的1px对应0.01rem,设计图的字体大小24px对应0.24rem,就是如此简单！
参考页面：
https://8.baidu.com/template/index/current.html
## 优化宽度问题
新增最大宽度，解决平板或手机横屏时体验不佳的问题
```javascript
window['adaptive'].maxWidth = 480; // 设置最大宽度，默认540px
```
需要css配合使用，添加如下代码：
```css
body {
    max-width: 6.4rem; // 设计图宽度为640px时为6.4rem ,750时为7.5rem ，以此类推
    margin: 0 auto;
}
body * {
    max-width: 6.4rem; // 设计图宽度为640px时为6.4rem ,750时为7.5rem ，以此类推
}
```

###使用方法：
```javascript
在页面head写入以下代码，实时更新html的fontsize:
<script src="js/adaptive.js"></script>  // 有缩放，精确还原设计图
<script src="js/adaptive-version2.js"></script> // 没有缩放，能快速开发的版本
<script src="js/adaptive-version3.js"></script> // 无论iphone还是安卓手机，都能精确还原1px
<script>
    window['adaptive'].desinWidth = 640;// 设计图宽度
    window['adaptive'].baseFont = 18;// 没有缩放时的字体大小
    window['adaptive'].maxWidth = 480;// 页面最大宽度 默认540
    window['adaptive'].init();// 调用初始化方法
</script>
```
然后在css中设置相应样式即可： 设计图的1px对应0.01rem,设计图的24px对应0.24rem,就是如此简单！
```css
.main-info {
    height: 0.88rem;
    padding-bottom: 0.24rem;
}
.fund-info {
    position: relative;
    font-weight: normal;
    padding: 0.2rem 0;
    padding-right: 1.7rem;
    padding-left: 0.23rem;
    font-size: 0.32rem;
    line-height: 1;
}
```
###adaptivejs原理：  

    利用rem布局，根据公式  
    
    html元素字体大小 = document根节点(html)宽度 * 100 / 设计图宽度  
    
    计算html元素的font-size,使1rem等于100px,方便快速开发  
    开发时，一个div设计图宽度为89px,那么在css中我们可以这样书写：width:0.89rem;  
    如果是文字，我们也建议使用rem。  
    
    对于iphone的retina高清显示屏，基本版本(adaptive.js)我们做了缩放处理，以达到最佳显示效果。 对于快速开发版本(adaptive-version2.js),viewport的width等于设备宽度，不会缩放 
    
###注意：如果设计图宽度大于document的宽度，0.01rem将小于1px,故如果设计图是1px,在css中仍然用1px显示。
 可用的全局变量：window.devicePixelRatioValue 当前页面设置的设备像素比

### 关于3个版本
```javascript
<script src="js/adaptive.js"></script>  // iphone下缩放，retina显示屏下能精确还原1px
<script src="js/adaptive-version2.js"></script> // 没有缩放，能快速开发的版本
<script src="js/adaptive-version3.js"></script> // 无论iphone还是安卓手机，都能精确还原1px，做到高度还原视觉稿 其中还提供了部分iphone手机下解决bug的方法
```
### chrome下rem字体偏大问题
通过reflow下外层元素能解决，比如加个高度什么的
