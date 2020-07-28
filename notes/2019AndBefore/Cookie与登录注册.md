## Cookie是什么

> **Cookie**（复数形态Cookies），中文名称为“小型文本文件”或“小甜饼”，指某些网站为了辨别用户身份而储存在用户本地终端（Client Side）上的数据（通常经过加密）。 —维基百科
>
> HTTP **Cookie**（也叫Web Cookie或浏览器Cookie）是服务器发送到用户浏览器并保存在本地的一小块数据，它会在浏览器下次向同一服务器再发起请求时被携带并发送到服务器上。通常，它用于告知服务端两个请求是否来自同一浏览器，如保持用户的登录状态。  —MDN

## Cookie的特点

1. 服务器通过 Set-Cookie 头给客户端一串字符串
2. 客户端每次访问相同域名的网页时，必须带上这段字符串
3. 客户端要在一段时间内保存这个Cookie
4. Cookie 默认在用户关闭页面后就失效，后台代码可以任意设置 Cookie 的过期时间
5. 大小大概在 4kb 以内

Q: 我在 Chrome 登录了得到 Cookie，用Safari访问, Safari会带上Cookie吗？

A: no

Q: Cookie存在哪里？

A: Window存在C盘的一个文件里

Q: Cookie可以作假吗？

A: sure

Q: Cookie有有效期吗？

A: 默认有效期20分钟左右，后段可以强制设置有效期

![](https://i.loli.net/2018/02/02/5a7410c627ed0.png)

## Set-Cookie

服务器在响应头部通过 **Set-Cookie**向客户端发送Cookie

### 语法(只写了常见的，详细请看[Set-Cookie](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Set-Cookie))

```
Set-Cookie: <cookie-name>=<cookie-value> 
Set-Cookie: <cookie-name>=<cookie-value>; Expires=<date>  
Set-Cookie: <cookie-name>=<cookie-value>; Max-Age=<non-zero-digit>
Set-Cookie: <cookie-name>=<cookie-value>; Domain=<domain-value>
Set-Cookie: <cookie-name>=<cookie-value>; Path=<path-value>
Set-Cookie: <cookie-name>=<cookie-value>; Secure
Set-Cookie: <cookie-name>=<cookie-value>; HttpOnly
```

**Expires**,Cookie的最长有效时间，形式为符合 HTTP-date 规范的时间戳。

**Max-Age**,在 Cookie 失效之前需要经过的秒数。

**Domain**,指定Cookie 可以送达的主机名。

**Path**,指定一个 URL 路径，这个路径必须出现在要请求的资源的路径中才可以发送 Cookie 首部。

**Secure **,一个带有安全属性的 cookie 只有在请求使用SSL和HTTPS协议的时候才会被发送到服务器。

**HttpOnly**,设置了 HttpOnly 属性的 cookie 不能使用 JavaScript 经由  Document.cookie属性、XMLHttpRequest 和  RequestAPIs 进行访问，以防范跨站脚本攻击（[XSS](https://developer.mozilla.org/en-US/docs/Glossary/XSS)）。

### 示例

```
HTTP/1.0 200 OK
Content-type: text/html
Set-Cookie: xxxxx_cookie=clyde; HttpOnly; Path=/    //此字段设置Cookie

[页面内容]
```

## Cookie 如何设置过期时间？

通过`Set-Cookie`响应头添加`Expires`或 `Max-Age`实现设置过期时间。

`Expires`接收符合`HTTP-date`规范的时间戳，告诉浏览器到什么时候Cookie都有效，时间受到本地设置时间影响（不稳定），

`Max-Age`接收秒数，让浏览器从收到消息多少时间内Cookie有效，

两者同时存在，`Max-Age`优先级更高。

例子: `Set-Cookie: namexxxx=xxxxxx; Max-Age= 8808293; Expires=Wed, 21 Oct 2018 07:28:00 GMT`

## 如何删除 Cookie？

// TODO

Cookie默认是在用户关闭页面后失效，

## 登录注册

### 登录

1. 浏览器（客户端）向服务端发送POST请求	,在请求头部第四部分携带数据

2. 服务端接收到数据，跟数据库中的数据进行比对

   --> 帐号密码跟数据库中的信息匹配，则在响应头部添加Set-Cookie，以后一段时间，浏览器发送请求头会带上Cookie

   --> 帐号密码跟数据库中的信息不匹配，则在响应头部中添加信息提示服务器，比如返回状态码4xx。

### 注册

跟登录类似