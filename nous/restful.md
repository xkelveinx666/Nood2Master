# Restful
Restful是流行的一种传输规范。使用Restful能让开发代码更通用。但是需要客户端和服务器一起遵守。以api接口优先，传输格式基本是JSON

- 一个URL代表一个一种资源
- 用某种表现载体来呈现这些资源
- 使用协议(GET、POST、PUT、DELETE])，将服务器的资源信息状态改变

> http://www.ruanyifeng.com/blog/2011/09/restful.html
> http://www.ruanyifeng.com/blog/2014/05/restful_api.html

## ContentType
每一个资源都有对应的Content-Type类型
|x-www-form-urlencoded|原生表单类型、或Get方式的提交|一般是key1=val1&key2=val2|
|multipart/form-data|POST的表单提交，修改过的表单提交|上传文件|
|application/json|json格式|灵活的以js对象方式请求|
|text/plain|纯文本格式|无格式化|

> http://www.ruanyifeng.com/blog/2008/06/mime.html

## 会话
客户端发出请求到服务端响应请求并断开连接前的的全过程
### Cookie
Cookie是服务器发给客户端的一小段信息，客户端可以暂时保存这些信息减少请求
### Session
每一个用户都有一个Session，不可以共享。根据sessionID来区分不同的用户。在断开连接前是不会释放session的，并且页面之间是共享的。可以保存用户数据减少请求。

> https://hit-alibaba.github.io/interview/basic/network/HTTP.html