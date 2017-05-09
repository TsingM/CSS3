# 自定义表单样式(radio/checkbox/select)
虽然HTML在其标签<input>的type属性中提供了关于单选框和复选框的实现方法，并有标签<select>用以实现下拉菜单，但是这些基础形态往往无法满足实际工作中的需求，而其中又封死了若干默认样式，导致我们在复写样式时束手束脚。与其纠缠不如另辟蹊径，下文将介绍这三种表单样式的自定义写法。

## 单选框 radio
单选框和复选框的核心思路类似，都是在原本的<input>之上用新的dom元素<label>覆盖，隐藏前者而在后者上实现我们想要的样式，两者通过id与for相互关联，多个radio之间通过name相互关联。HTML片段如下：
```html
<div class="nm-radio">
    <input type="radio" id="radio1" name="radio" checked="checked"/>
    <label for="radio1"></label>
</div>
```
CSS的重点就在于<label>的样式实现上，已笔者当前所写系统样式为例，需要实现一个圆环内包含一个实心圆的样式，实心圆显示时为选中状态，CSS3的border-radius可以轻松实现，这里将实心圆放在了label的before伪元素上：
```css
.nm-radio {
    position: relative;
    width: 16px;
    height: 16px;
}
.nm-radio input {
    position: absolute;
    visibility: hidden
}
.nm-radio label {
    position: absolute;
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 1px solid #d7d7d7;
    border-radius: 9px;
}
/*选中状态*/
.nm-radio input:checked + label {
    border: 1px solid #1baede;
}
.nm-radio input:checked + label:before {
    content: "";
    position: absolute;
    top: 3px; left: 3px;
    width: 10px;
    height: 10px;
    border-radius: 5px;
    background-color: #1baede;
}
```
如果项目还需要实现禁用状态的话，在此基础上加一些样式覆盖即可：
```css
/*禁用状态*/
.nm-radio input:disabled + label {
    border: 1px solid #d7d7d7;
}
.nm-radio input:disabled + label:before {
    background-color: #d7d7d7
}
```
---
## 复选框 checkbox
相较于单选框，复选框的实现虽然类似，但略复杂一些，主要体现在那个“勾”的实现上。先上基础的CSS代码：
```css
.nm-checkbox {
    position: relative;
    width: 16px;
    height: 16px;
}
.nm-checkbox input {
    position: absolute;
    visibility: hidden;
}
.nm-checkbox label {
    position: absolute;
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 1px solid #d7d7d7;
}
```
当复选框处于选中状态时，首先要改变其边框颜色和背景色，然后在中间显示出表示选中的勾，这个通过CSS3中2D转换的rotate实现，即绘制一个空心的长方形框并只显示其两条边，再将它进行一定角度的旋转，便能完美地做出一个勾的形状了，这里将背景层放在before伪元素上、勾放在after伪元素上。
```css
/*选中状态*/
.nm-checkbox input:checked + label {
    border: 1px solid #1baede;
}
.nm-checkbox input:checked + label:before {
    content: "";
    position: absolute;
    width: 16px;
    height: 16px;
    background-color: #1baede;
}
.nm-checkbox input:checked + label:after {
  content: "";
  position: absolute;
  left: 2px;bottom: 6px;
  width: 8px;height: 4px;
  border: 2px solid #ffffff; border-top-color: transparent; border-right-color: transparent;
  -ms-transform: rotate(-60deg); -moz-transform: rotate(-60deg); -webkit-transform: rotate(-60deg); transform: rotate(-45deg);
}
```
禁用状态的实现也与radio类似：
```css
/*禁用状态*/
.nm-checkbox input:disabled + label {
    border: 1px solid #d7d7d7;
}
.nm-checkbox input:disabled + label, .nm-checkbox input:disabled + label:before {
    background-color: #d7d7d7;
}
```

## 下拉菜单 select
在实现自定义下拉框时完全抛弃了<select>，而是用一个<input>和一个<ul>来模拟出它的样子，当然用<input>是为了支持可输入，如果不需要输入的话随便一些其他标签也可以，另外还需要一个标签<i>来模拟下拉的那个小箭头：
```html
<div class="nm-select">
    <i></i>
    <input type="text" />
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>
</div>
```
具体样式可根据需求调整：
```css
.nm-select {
    position: relative;
}
.nm-select input {
    height: 36px;
    width: 100%;
    padding: 3px 20px;
    margin: 0;
    border: 1px solid #cecece;
    border-radius: 4px;
    color: #333;
    box-sizing: border-box;
    font-size: 16px;
}
.nm-select i {
    position: absolute;
    top: 15px; right: 10px;
    width: 0; height: 0;
    border: 5px solid transparent;
    border-top-color: #b4b4b4;
    cursor: pointer
}
.nm-select ul {
    display: none;
    overflow: hidden;
    width: 100%;
    padding: 0;
    padding: 5px 0;
    margin: 2px 0 0 0;
    border: 1px solid #cecece;
    border-radius: 4px;
    box-shadow: 0 6px 12px rgba(0,0,0,.175)
}
.nm-select ul li {
    padding: 3px 20px;
    margin: 0;
    cursor: pointer;
    color: #333333;
}
.nm-select ul li:hover {
    background-color: #e9f7fc;
}
```
实际应用中将通过MVVM框架的双向绑定以及jquery来实现下拉框的赋值和动效，不在CSS的能力范围内，而这里可以先通过focus伪类来控制简单的显隐，以一个dom元素的事件来控制另一个元素的显隐，也算是一个小技巧：
```css
.nm-select input:focus + ul {
    display: block
}
```

其实只要明白主要思路，实现起来都是非常简单的事情。