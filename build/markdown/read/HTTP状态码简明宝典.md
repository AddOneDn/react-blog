## 介绍
状态码的职责是当客户端向服务端发送请求时候，描述返回的请求内容

> 状态码如200 OK ，以三位数字和原因短语组成

| 状态码        | 类别           | 原因短语  |
| ------------- |:-------------:| :-----:|
| 1XX    | informational(信息性状态码) | 接收的请求正在处理 |
| 2XX | Success(成功状态码) | 请求正常处理完毕 |
| 3XX | Redirection(重定向状态码) | 需要进行附加操作以完成请求 |
| 4XX | Client Error(客户端错误状态码) | 服务器无法处理请求 |
| 5XX | Server Error(服务器错误状态码) | 服务器处理请求出错 |
本文只介绍具有代表性的14个状态码

## 2XX成功

2XX的响应结果表明请求被正常处理了

### 200 OK

从客户端发来的请求在服务端被正常处理了

> 在响应报文内，随状态码一起返回的信息会因方法的不同而发生改变(GET/HEAD)

### 204 No Content

服务器接收的请求已成功处理，但在返回的响应报文中不含实体的主体部分，也不允许返回任何实体的主体

> 一般在只需要从客户端往服务端发送信息，而对客户端不需要发送新信息内容的情况下使用

### 206 Partial Content

客户端进行了范围请求，而服务器成功执行了这部分的GET请求

> 响应报文中包含由Content-Range指定范围的实体内容

## 3XX 重定向

3XX的响应结果表明浏览器需要执行某些特殊的处理来正确处理请求

### 301 Moved Permanently

永久性重定向。请求的资源已经被分配了新的URI，以后应该使用资源现在所指向的URI

> 如果已经把资源对应URI保存为书签，这时应该按Location首部字段提示的URI重新保存

### 302 Found

临时性重定向。请求的资源已经被分配了新的URI，希望用户(本次)使用新的URI访问

> 只是临时性质的移动。如果已经把URI保存为书签，不会像301那样去更新，而是仍旧保留返回302状态码的页面对应URI

### 303 See Other

请求对应的资源存在着另一个URI，应使用GET方法定向获取请求资源。

> 303与302有相同的功能，但是303明确表明应该使用GET方法

### 304 Not Modified

客户端发送附带条件的请求时，服务器允许请求访问资源。但若请求未满足条件，则直接返回304(服务端资源未改变，可直接使用客户端未过期的缓存)

### 307 Temporary Redirect

临时重定向。与302 Found有相同的含义

> 307会遵照浏览器标准，不会从POST变成GET

## 4XX 客户端错误

4XX的响应结果表明客户端是发生错误的原因所在

### 400 Bad Request

请求报文中存在语法错误，需修改请求内容再次发送

> 浏览器会像对待200 OK一样对待该状态码

### 401 Unauthorized

发送的请求需要有通过HTTP认证的认证信息，若之前已进行过一次请求，则表示认证失败。

> 返回该响应必须包含一个适用于被请求资源的WWW-Authenticate首部以质询用户信息。
浏览器初次接收到401响应会弹出认证用的对话窗口

### 403 Forbidden

请求资源的访问被服务器拒绝。服务器没有必要给出拒绝的详细理由。

> 未获得文件系统的访问授权，访问权限出现某些问题等情况都有可能触发403

### 404 Not Found

服务器上无法找到请求的资源

> 也可在服务端拒绝请求且不想说明理由时使用

## 5XX 服务器错误
5XX的响应结果表明服务器本身发生错误

### 500 Internal Server Error

服务端在执行请求时发生了错误，也有可能是Web应用的Bug或临时故障

### 503 Service Unavailable

服务器处于超负载或正在停机维护，无法处理请求。

## 补充

+ 返回的状态码可能和信息不对等
+ URI是什么?


> 参考于《HTTP图解》

