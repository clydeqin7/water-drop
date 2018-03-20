# JSONP、CORS 、postMessage

## 同源政策

同源政策（same-origin policy)的含义是A网页设置的Cookie, B网站不能打开，除非这两个网页“同源”。"同源"指的是“三个相同”

- 协议相同    如：`http://`
- 域名相同    如：` www.example.com`
- 端口相同    如：`80` (默认端口可以省略)

### 目的

同源政策的目的，是为了保证用户信息的安全，防止恶意的网站窃取数据。

### 限制范围

1. Cookie、LocalStorage 和 IndexDB 无法读取。
2. DOM 无法获得。
3. AJAX 请求不能发送。

这3种限制都是可以规避，详见[浏览器同源政策及其规避方法-阮一峰](http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html)，下文将主要介绍JSONP、CROS、postMessage三种方式。

## JSONP

JSONP是服务器与客户端跨源通信的常用方法。网页通过添加一个`<script>`元素，向服务器请求JSON数据，这种做法不受同源政策限制；服务器收到请求后，将数据放在一个指定名字的回调函数里传回来。

```javascript
function addScriptTag(src) {
  var script = document.createElement('script');
  script.setAttribute("type","text/javascript");
  script.src = src;
  document.body.appendChild(script);
}

window.onload = function () {
  addScriptTag('http://example.com/ip?callback=foo');
}

function foo(data) {
  console.log('Your public IP address is: ' + data.ip);
};
```

### 什么是JSONP

> 1. 请求方(浏览器）创建script,src指向响应方（服务器），同时传一个查询参数?callback=yyy;
> 2. 响应方根据查询参数callback，构造形如
>    1. yyy.call(undefined, '你要的数据'),
>    2. yyy('你要的数据')的响应,
> 3. 请求方接收到响应后，就会执行yyy.call(undefined, '你要的数据'), 
> 4. 请求方就知道自己所需要的数据了。

![](https://i.loli.net/2018/01/07/5a52204573630.png)

**jQuery用法**

```
 $.ajax({
 url: "http://jack.com:8002/pay",
 dataType: "jsonp",
 success: function( response ) {
     if(response === 'success'){
     	amount.innerText = amount.innerText - 1
     }
 }
 })
```

### JSONP为什么不支持POST?

1. JSONP是动态创建script实现的。
2. 动态创建script只能用get请求无法用post请求。

## CORS

> [跨域资源共享 CORS 详解-阮一峰](http://www.ruanyifeng.com/blog/2016/04/cors.html)

CORS是一个W3C标准，全称是"跨域资源共享"（Cross-origin resource sharing）。

CORS需要浏览器和服务器同时支持。目前，所有浏览器都支持该功能，IE浏览器不能低于IE10。

整个CORS通信过程，都是浏览器自动完成，不需要用户参与。对于开发者来说，CORS通信与同源的AJAX通信没有差别，代码完全一样。浏览器一旦发现AJAX请求跨源，就会自动添加一些附加的头信息，有时还会多出一次附加的请求，但用户不会有感觉。

因此，实现CORS通信的关键是服务器。只要服务器实现了CORS接口，就可以跨源通信。

### 两种请求

浏览器将CORS请求分成两类：简单请求（simple request）和非简单请求（not-so-simple request）。

#### 简单请求

只要**同时满足**以下两大条件，就属于简单请求。

> （1) 请求方法是以下三种方法之一：
>
> - HEAD
> - GET
> - POST
>
> （2）HTTP的头信息不超出以下几种字段：
>
> - Accept
> - Accept-Language
> - Content-Language
> - Last-Event-ID
> - Content-Type：只限于三个值`application/x-www-form-urlencoded`、`multipart/form-data`、`text/plain`

#### 非简单请求

凡是**不同时满足**上面两个条件，就属于非简单请求。

### 简单请求的处理

对于简单请求，浏览器直接发出CORS请求。具体来说，就是在头信息之中，增加一个`Origin`字段。

```http
GET /cors HTTP/1.1
Origin: http://api.bob.com
Host: api.alice.com
Accept-Language: en-US
Connection: keep-alive
User-Agent: Mozilla/5.0...
```

`Origin`字段用来说明，本次请求来自哪个源（协议 + 域名 + 端口）。服务器根据这个值，决定是否同意这次请求。

如果`Origin`指定的源，不在许可范围内，服务器会返回一个正常的HTTP回应。浏览器发现，这个回应的头信息没有包含`Access-Control-Allow-Origin`字段（详见下文），就知道出错了，从而抛出一个错误，被`XMLHttpRequest`的`onerror`回调函数捕获。注意，这种错误无法通过状态码识别，因为HTTP回应的状态码有可能是200。

如果`Origin`指定的域名在许可范围内，服务器返回的响应，会多出几个头信息字段。

```http
Access-Control-Allow-Origin: http://api.bob.com
Access-Control-Allow-Credentials: true
Access-Control-Expose-Headers: FooBar
Content-Type: text/html; charset=utf-8
```

**（1）Access-Control-Allow-Origin**

该字段是必须的。它的值要么是请求时`Origin`字段的值，要么是一个`*`，表示接受任意域名的请求。

**（2）Access-Control-Allow-Credentials**

该字段可选。它的值是一个布尔值，表示是否允许发送Cookie。默认情况下，Cookie不包括在CORS请求之中。设为`true`，即表示服务器明确许可，Cookie可以包含在请求中，一起发给服务器。这个值也只能设为`true`，如果服务器不要浏览器发送Cookie，删除该字段即可。

**（3）Access-Control-Expose-Headers**

该字段可选。CORS请求时，`XMLHttpRequest`对象的`getResponseHeader()`方法只能拿到6个基本字段：`Cache-Control`、`Content-Language`、`Content-Type`、`Expires`、`Last-Modified`、`Pragma`。如果想拿到其他字段，就必须在`Access-Control-Expose-Headers`里面指定。上面的例子指定，`getResponseHeader('FooBar')`可以返回`FooBar`字段的值。

### 非简单请求的处理

非简单请求是那种对服务器有特殊要求的请求，比如请求方法是`PUT`或`DELETE`，或者`Content-Type`字段的类型是`application/json`。

非简单请求的CORS请求，会在正式通信之前，增加一次HTTP查询请求，称为"预检"请求（preflight）。

浏览器先询问服务器，当前网页所在的域名是否在服务器的许可名单之中，以及可以使用哪些HTTP动词和头信息字段。只有得到肯定答复，浏览器才会发出正式的`XMLHttpRequest`请求，否则就报错。

```http
OPTIONS /cors HTTP/1.1   //"预检"请求用的请求方法是OPTIONS，表示这个请求是用来询问的
Origin: http://api.bob.com 
Access-Control-Request-Method: PUT //该字段是必须的，用来列出浏览器的CORS请求会用到哪些HTTP方法
Access-Control-Request-Headers: X-Custom-Header //该字段是一个逗号分隔的字符串，指定浏览器CORS请求会额外发送的头信息字段
Host: api.alice.com
Accept-Language: en-US
Connection: keep-alive
User-Agent: Mozilla/5.0...
```

## CORS与JSONP的比较

CORS与JSONP的使用目的相同，但是比JSONP更强大。

JSONP只支持`GET`请求，CORS支持所有类型的HTTP请求。JSONP的优势在于支持老式浏览器，以及可以向不支持CORS的网站请求数据。

## postMessage

`window.postMessage`是HTML5引入的全新的API, 可以安全地实现跨源通信。

举例来说，父窗口`http://aaa.com`向子窗口`http://bbb.com`发消息，调用`postMessage`方法就可以了。

```javascript
var popup = window.open('http://bbb.com', 'title');
popup.postMessage('Hello World!', 'http://bbb.com');
```

`postMessage`方法的第一个参数是具体的信息内容，第二个参数是接收消息的窗口的源（origin），即"协议 + 域名 + 端口"。也可以设为`*`，表示不限制域名，向所有窗口发送。

子窗口向父窗口发送消息的写法类似。

```javascript
window.opener.postMessage('Nice to see you', 'http://aaa.com');
```

父窗口和子窗口都可以通过`message`事件，监听对方的消息。

```javascript
window.addEventListener('message', function(e) {
  console.log(e.data);
},false);
```

`message`事件的事件对象`event`，提供以下三个属性。

- `event.source`：发送消息的窗口
- `event.origin`: 消息发向的网址
- `event.data`: 消息内容

下面的例子是，子窗口通过`event.source`属性引用父窗口，然后发送消息。

```javascript
window.addEventListener('message', receiveMessage);
function receiveMessage(event) {
  event.source.postMessage('Nice to see you!', '*');
}
```

`event.origin`属性可以过滤不是发给本窗口的消息。

```javascript
window.addEventListener('message', receiveMessage);
function receiveMessage(event) {
  if (event.origin !== 'http://aaa.com') return;
  if (event.data === 'Hello World') {
      event.source.postMessage('Hello', event.origin);
  } else {
    console.log(event.data);
  }
}
```

