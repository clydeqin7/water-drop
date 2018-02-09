## Session是什么

**服务器上的哈希表**

1. 将 SessionID (随机数)通过 Cookie 发给客户端

2. 客户端访问服务器时，服务器读取 SessionID

3. 服务器有一块内存（哈希表）保存了所有 Session

4. 通过 SessionID 我们可以得到对应用户的隐私信息，如 id, email

5. 这块内存(哈希表)就是服务器上的所有 session

   ​

**一般来说，Session 基于 Cookie 来实现。**

![](https://i.loli.net/2018/02/05/5a77b3ba4a8f8.png)

## LocalStorage是什么

**浏览器上的hash表**, HTML5新提供的API,window系统是存在C盘的文件实现持久化存储。

### 常用方法

#### setItem()

接受一个键名和值作为参数，将会把键名添加到存储中，如果键名已存在，则更新其对应的值

```
storage.setItem(keyName, keyValue)
```

#### getItem()

接受一个键名（key name）作为参数，并返回对应键名的值（key's value）

```
storage.getItem(keyName, keyValue)
```

#### clear()

调用它可以清空存储对象里所有的键值

```
storage.clear()
```

### 特点

1. LocalStorage 跟 HTTP 无关
2. HTTP 不会带上 LocalStorage 的值
3. 只有相同域名的页面才能互相读取 LocalStorage（但是没有同源那么严格）
4. 每个域名 LocalStorage 最大存储量为 5MB 左右（每个浏览器不一样）
5. 常用场景：记录有没有提示过用户（没有用的或者说是不敏感的信息）
6. LocalStorage 永久有效, 除非用户清除数据

## LocalStorage与Cookie的区别

1. 2者在window系统都是存在C盘的一个文件里的,都能进行数据存储
2. Cookie是属于HTTP里的
3. LocalStorage是HTML5提供的一个API
4. Cookie大小4KB左右，LocalStorage大小5MB左右

## SessionStorage是什么

### 特点

​	1-4点同LocalStorage的特点1-4相同

​	5. 页面关闭（session结束后）后就会失效

## Cache-Control是什么

HTTP设置缓存的一种方法，在HTTP请求和响应中通过**Cache-Control**通用消息头设置来实现缓存。

### 语法

[语法详见MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Cache-Control)

```
Cache-Control: max-age=<seconds>  // 过了多久时间过期
```

### tips

1. **max-age**设置很长时间（1年-10年），如果服务器资源有更新，通过URL请求的查询参数变化获取新资源

   ```
   xxxx.com/login_in?jdksf_v2
   ```

   ​

## Expires是什么

HTTP设置缓存的一种方法，在HTTP请求和响应中通过**Expires**通用消息头设置来实现缓存。

如果还有一个 设置了 "max-age" 或者 "s-max-age" 指令的**Cache-Control**响应头，那么**Expires**头就会被忽略。

### 语法

```
Expires: <http-date>  // 到了什么时候过期，基于本地时间
// 举个栗子
Expires: Wed, 21 Oct 2018 07:28:00 GMT
```

## ETag缓存验证

[HTTP ETag-维基百科](https://zh.wikipedia.org/wiki/HTTP_ETag)

[MD5消息摘要算法-维基百科](https://zh.wikipedia.org/wiki/MD5)，文件相同，MD5（文件）的散列值一致

### 典型应用

当一个URL被请求，服务器返回资源和其对应的ETag值（MD5(文件)生成的散列值），放入HTTP响应头部的**ETag**字段

```
协议/版本号 状态码 状态解释
2 Key1: value1
2 Key2: value2
2 Content-Length: 17931
2 Content-Type: text/html
2 Etag: "686897696a7c876b7e"
3
4 要下载的内容
```

然后，客户端可以决定是否缓存这个资源和它的ETag。以后，如果客户端想再次请求相同的URL，将会发送一个包含已保存的ETag和**If-None-Match**字段的请求。

```
1 动词 路径 协议/版本
2 Key1: value1
2 Key2: value2
2 Content-Type: application/x-www-form-urlencoded
2 If-None-Match: "686897696a7c876b7e"
3 
4 要上传的数据
```

服务器接收请求后，比较客户端的ETag和当前版本资源的ETag的值，匹配则资源没有修改，服务器则返回状态码为 **304 Not Modified** 的HTTP响应，提示客户端本地缓存的资源是最新的，没有修改可以直接使用。

## HTTP缓存（Cache-Control、Expires)与304的区别

> [HTTP缓存控制小结-孙世吉](http://imweb.io/topic/5795dcb6fb312541492eda8c)

1. 在URI输入栏中输入然后回车

   返回状态码**200 OK (from cache)**浏览器发现该资源已经缓存了而且没有过期, 会不跟服务器确认直接使用浏览器缓存的内容。

2. F5/点击工具栏中的刷新按钮/右键菜单重新加载

   F5的作用和直接在URI输入栏中输入然后回车是不一样的，F5会让浏览器**无论如何都发一个HTTP Request给Server**，即使先前的响应中有Expires头部。

3. Ctrl+F5

   Ctrl+F5要的是**彻底的从Server拿一份新的资源过来**, 请求头部里不会带If-Modified-Since/If-None-Match消息头，服务器响应成功会返回**200 OK**

   ​