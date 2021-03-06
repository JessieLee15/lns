# Tips

## 浏览器拦截window.open
`window.open`如果不是在用户触发的事件内部，会被浏览器拦截（各种异步操作内部，最常见的如ajax）

浏览器这样做也是非常可以理解的，只有用户可以自发地打开新页面；防止恶意代码和广告

___解决：__

使用隐藏标签a或button
[解决办法] (https://www.cnblogs.com/digdeep/p/4590337.html?tvd)

[触发a标签跳转] (https://blog.csdn.net/aopao1/article/details/75258129)

___


## 有毒的HTML转义字符-&#8236

现象：不知道用户以哪种方式剪切的数据，或者中间经过了什么转发，导致（微信）粘贴到mis这边的数据多了一个HTML的非常特殊的转义字符`&#8236`（猜测是个占位符），encodeURL后是`%E2%80%AC`

目前没有找到在js中处理这个字符的方法，可以人为处理 - 粘贴后敲一下删除可以把最后一个字符删掉

参考文章：
[html】input标签value属性值的字符长度多了1的诡异bug] (https://blog.csdn.net/w390058785/article/details/80692930)

___

## 浏览器打印

起因说明：做一个100*70的打印签（用到了JsBarcode插件，注意JsBarcode有默认的margin）。关键是打印大小的调整

总结：
 1. chrome对字体设置的处理：12px以下的字体实际都显示为12px。
    > 解决方案：
      老版本WebKit支持`-webkit-text-size-adjust: none;`的设置；

      新版本通过`-webkit-transform: scale(0.75)`设置缩放解决（可设置局部缩放）;缩放产生的空白通过设置margin为负解决;

2. 打印样式通过`@media print`设置，只在打印时生效
3. 打印区域设置的背景样式需要在打印时勾选【打印背景】才会有效果；注意hr标签也是背景（可以通过设置其他标签border模拟hr效果）