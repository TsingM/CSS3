# 媒体查询综述
媒体查询可以让我们根据设备显示器的特性（如视口宽度、屏幕比例、设备方向：横向或纵向）为其设定CSS样式，媒体查询由媒体类型和一个或多个检测媒体特性的条件表达式组成。媒体查询中可用于检测的媒体特性有 width、height、aspect-ratio等。使用媒体查询，可以在不改变页面内容的情况下，为特定的一些输出设备定制显示效果。
---
#兼容性设置
1. 兼容移动设备
```html
<name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
```
- width = device-width：宽度等于当前设备的宽度
- initial-scale： 初始的缩放比例（默认设置为1.0）
- maximum-scale：允许用户缩放到的最大比例（默认设置为1.0）
- user-scalable：用户是否可以手动缩放（默认设置为no，因为不希望用户放大缩小页面）
2. 兼容低版本IE
```html
<!--[if lt IE 9]-->
<script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
<script src="https://oss.maxcdn.com/libs/respond.js/1.3.0/respond.min.js"></script>
<!--[endif]-->
<meta http-equiv="X-UA-Compatible" ;content="IE=edge, chrome=1">
```
如果不是完全响应式布局而只考虑移动端开发，则不需要进行兼容性设置，移动端浏览器基本都是webkit内核。
---
#CSS媒体查询
