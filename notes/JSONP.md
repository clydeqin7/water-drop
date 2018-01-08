# JSONP

## 什么是JSONP?

![课程截图](https://i.loli.net/2018/01/07/5a52204573630.png)

请求方(浏览器）创建script,src指向响应方（服务器），同时传一个查询参数?callback=yyy;响应房根据查询参数callback，构造形如1.yyy.call(undefined, '你要的数据'), 2.yyy('你要的数据')的响应, 3.请求方接收到响应后，就会执行yyy.call(undefined, '你要的数据'), 4.请求方就知道自己所需要的数据了。

## JSONP为什么不支持POST?

1. JSONP是动态创建script实现的
2. 动态创建script只能用get请求无法用post请求