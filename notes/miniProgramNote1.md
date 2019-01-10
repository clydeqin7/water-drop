```
title: 小程序笔记1
```

[微信开发者工具快捷键](https://developers.weixin.qq.com/miniprogram/dev/devtools/shortcut.html)

# 小程序线程架构

## 生命周期

小程序完整的生命周期示例：

![完整生命周期示例](https://i.loli.net/2019/01/08/5c341c5eddb0b.png)

```
onLoad: function() { //页面加载时执行的初始化工作 }
onReady: function() { //页面就绪后触发执行的操作 }
onShow: function() { //页面打开时，触发执行的操作 }
onHide: function() { //页面隐藏时，触发执行的操作 }
onUnload: function() { //页面关闭时触发执行的操作 }
```

一个page的生命周期从`onLoad`开始，整个生命周期内`onLoad`、`onReady`、`onUnload`这三个事件**只执行一次**，而`onHide`和`onShow`在**每次页面隐藏和显示时都会触发**。

## 线程架构

```
view线程（wxss+wxml）
appServer线程（JS）
```
# 数据绑定

## 简单绑定

使用Mustache语法（即“双大括号”语法）将变量包起来，可以作用于：

1. 内容：

```
<!-- wxml -->
<view>{{ content }}</view>
//page.js
Page({
  data: {
    content: 'Hello MiniApp!'
  }
})
```

2. 组件属性（需在双引号之内）：

```
<!-- wxml -->
<view id="item-{{id}}"></view>
//page.js
Page({
  data: {
    id: 0
  }
})
```

3. 控制属性（需在双引号之内）：

```
<!-- wxml -->
<view wx:if="{{condition}}"></view>
//page.js
Page({
  data: {
    condition: true
  }
})
```

## 运算

可以在`{{}}`内进行简单的运算。如：

```
<view hidden="{{flag ? true : false}}"> Hidden </view>
<view> {{a + b}} + {{c}} + d </view>
```

## 组合

可以在`{{}}`内直接进行组合，构成新的对象或者数组。

# 条件语句

1. `wx:if`

```
<view wx:if="{{length > 5}}">1</view>
<view wx:elif="{{length > 2}}">2</view>
<view wx:else>3</view>
```

2. `block wx:if`

```
<block wx:if="{{true}}">
  <view>1</view>
  <view>2</view>
</block>
```

3. `wx:if` VS `hidden`

`wx:if`是惰性的，只有在条件第一次变成真的时候才开始局部渲染。

`hidden`则是始终会被渲染。

`wx:if`有更高的切换消耗，`hidden`有更高的初始渲染消耗。需要频繁切换的场景使用`hidden`更好，如果运行时条件不大可能改变，则`wx:if`较好。

# 列表语句

1. `wx:for`

在组件上使用`wx:for`控制属性绑定一个数组，使用数组中各项数据重复渲染该组件。默认数组当前项的下标变量名默认为index，数组当前项的变量名默认为item。

```
<view wx:for="{{items}}">
  {{index}}: {{item.message}}
</view>
//page.js
Page({
  data: {
    items: [{
      message: 'foo'
    }, {
      message: 'bar'
    }]
  }
})
```

使用`wx:for-item`可以指定数组当前元素的变量名。

使用`wx:for-index`则可以指定数组当前下标的变量名

```
<view wx:for="{{items}}" wx:for-item="itemName" wx:for-index="idx">
  {{idx}}: {{itemName.message}}
</view>
```

`wx:for`可以嵌套。

2. `block wx:for`

```

```

# 引用

import和include。import可以在改文件使用目标文件定义的template，但不会引用目标文件嵌套import的template。include可将目标文件除模板代码(<template/>)块的所有代码引入，相当于拷贝到include位置。

# 事件绑定

# 页面配置~page.json

页面的.json文件只能配置window配置项，以决定本页面的窗口表现，所以配置中也无需写window这个键值。

# 尺寸单位与适配

## 尺寸单位

WXSS新增了针对移动端屏幕的两种尺寸单位：rpx和rem。

**rpx(responsive pixel)**：可以根据屏幕宽度进行自适应。规定屏幕宽为750rpx。如在iPhone6上，屏幕宽度为375px，共有750个物理像素，则750rpx = 375px = 750物理像素，1rpx = 0.5px = 1物理像素。

**rem(root em)**：规定屏幕宽度为20rem；1rem = (750/20) rpx。

## 适配

rpx计量最大的优势在于750设计稿不需要进行任何转换即可适配。在WXSS中并不支持算术运算符，所以小程序的视觉设计稿尽量使用750给出。
