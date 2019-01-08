```
title: 小程序笔记1
```

[微信开发者工具快捷键](https://developers.weixin.qq.com/miniprogram/dev/devtools/shortcut.html)

# 小程序线程架构

### 生命周期

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

### 线程架构

```
view线程（wxss+wxml）
appServer线程（JS）
```
