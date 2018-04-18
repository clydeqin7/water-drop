# Bootstrap初体验

**Bootstrap**是Twitter推出的一个用于前端开发的开源工具包。用于开发响应式布局、移动设备优先的 WEB 项目。

## 媒体查询

```
/* 超小屏幕（手机，小于 768px） xs */
/* 没有任何媒体查询相关的代码，因为这在 Bootstrap 中是默认的（还记得 Bootstrap 是移动设备优先的吗？） */

/* 小屏幕（平板，大于等于 768px）sm */
@media (min-width: @screen-sm-min) { ... }

/* 中等屏幕（桌面显示器，大于等于 992px）md */
@media (min-width: @screen-md-min) { ... }

/* 大屏幕（大桌面显示器，大于等于 1200px）lg */
@media (min-width: @screen-lg-min) { ... }
```

## 栅格系统

[栅格系统](https://v3.bootcss.com/css/#grid)

Bootstrap 提供了一套响应式、移动设备优先的流式栅格系统，随着屏幕或视口（viewport）尺寸的增加，系统会自动分为最多12列。