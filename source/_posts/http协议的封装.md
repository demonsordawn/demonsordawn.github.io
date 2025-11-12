---
title: "HTTP协议的封装"
tag: 'HTTP'
---

## HTTP协议的封装
 - 应用层：    HTTP 报文 (HTTP Message)
 -            ↓
 - 安全层：    TLS/SSL 加密 (HTTPS 情况下)
 -             ↓
 - 传输层：    TCP 段 (TCP Segment)
 -             ↓
 - 网络层：    IP 数据包 (IP Packet)
 -             ↓
 - 链路层：     以太网帧/PPP帧等 (Data Link Frame)
 -             ↓
 - 物理层：      比特流 (Bits)

###  http请求消息request
- 请求行: 用来说明请求类型,要访问的资源以及所使用的http版本
- 请求头部: 用来说明服务器要使用的附加信息(请求头和请求体之间一定有一行空格)
- 请求体: 即请求数据,可以添加任意的其他数据

### http响应消息response
- 响应行,响应头,空行,响应体 (响应头和响应体之间一定有一行空格,即使响应数据为空,也必须有空行)
- 响应行: 也叫状态行,由HTTP协议版本号,状态码,状态信息三部分组成.
- 响应头: 用来说明服务器响应的一些信息,比如内容类型,内容长度,服务器信息等.
- 空行: 用来分隔响应头和响应体.
- 响应体: 服务器返回的具体内容,可以是html页面,图片,视频,音频等.

### 常见的响应状态及其含义
- 1xx: 指示信息--表示请求已接收,继续处理
- 2xx: 成功--表示请求已成功被服务器接收,理解,并接受
- 3xx: 重定向--要完成请求必须进行更进一步的操作
- 4xx: 客户端错误--请求有语法错误或请求无法实现
- 5xx: 服务器错误--服务器未能实现合法-
- 100 Continue: 服务器仅接收到部分请求,要求客户端继续发送其余部分.
- 101 Switching Protocols: 服务器转换协议,正在进行切换.
- 200 OK: 请求成功.
- 201 Created: 已创建新资源.
- 202 Accepted: 已接受请求,但未处理完成.
- 204 No Content: 服务器成功处理了请求,但没有返回任何内容.
- 301 Moved Permanently: 所请求的页面已经转移至新的url.
- 302 Found: 所请求的页面临时转移至新的url.
- 304 Not Modified: 未修改页面,可使用缓存.
- 400 Bad Request: 服务器未能理解请求.
- 401 Unauthorized: 请求未经授权.
- 403 Forbidden: 禁止访问.
- 404 Not Found: 服务器无法找到请求的页面.
- 405 Method Not Allowed: 请求方法不被允许.
- 406 Not Acceptable: 服务器无法满足客户端请求的Accept头.
- 408 Request Timeout: 服务器等待客户端发送的请求时间过长.
- 411 Length Required: 服务器无法处理客户端发送的不带Content-Length的请求信息.
- 413 Payload Too Large: 服务器无法处理请求,因为请求实体过大.
- 414 URI Too Long: 请求的URI过长.
- 415 Unsupported Media Type: 服务器无法处理请求,因为媒体格式不支持.
- 417 Expectation Failed: 服务器未满足Expect的请求头信息.
- 500 Internal Server Error: 服务器遇到错误,无法完成请求.
- 501 Not Implemented: 服务器不支持请求的功能.
- 503 Service Unavailable: 由于超载或系统维护,服务器暂时的无法处理客户端的请求.
- 504 Gateway Timeout: 网关超时.

### 常见的http头
- content-type: 数据类型(text/html)
- content-length: body的长度
- host:客户端告知服务器,所请求的资源是在哪个主机的哪个端口上
- user-agent: 声明用户的操作系统和浏览器版本信息
- referer: 记录从哪个页面链接访问过来的
- loaction: 记录用户当前所在的位置
- Cookie: 用于在客户端存储少量信息通常用于实现会话(session)的功能

### https
- https是http协议的安全版本,它是建立在ssl/tls协议之上的.
- https协议的主要作用是:
- 1. 建立一个信息安全通道,通过对网络通信进行加密保护,防止数据泄露,确保数据完整性.
- 2. 验证服务器的身份,确保服务器可信.
- 3. 保护用户的个人信息,防止数据泄露.
- 4. 保护网络通讯的隐私和安全.

### http完整请求过程
1. DNS域名解析,拿到ip地址进行访问
2. 建立TCP连接,三次握手
3. HTTP协议request内容发送(首行,head,空行,body)
4. 服务器接收到请求,并进行相应的业务处理(浏览器得到html代码)
5. 服务器端将结果返回给客户端
6. 浏览器拿到返回结果,并调用浏览器的内核进行前端页面的渲染
7. TCP连接断开,四次挥手