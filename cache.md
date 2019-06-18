# 缓存
## 强缓存
一般存于内存，读取速度快，报文中显示from memory cache

* ### expires 
Expires: Wed, 22 Oct 2018 08:41:00 GMT 表示资源会在 `Wed, 22 Oct 2018 08:41:00 GMT` 后过期，需要再次请求

* ### Cache-control
Cache-control: max-age=30 该属性表示资源会在 30 秒后过期，需要再次请求。该属性还存在多种属性值如`no-cache` `no-store` `public`等

## 协商缓存
如果缓存过期了，我们就可以使用协商缓存来解决问题。协商缓存需要请求，如果缓存有效会返回 304。协商缓存需要客户端和服务端共同实现，和强缓存一样，也有两种实现方式。 

* ### Last-Modified 和 If-Modified-Since
`Last-Modified` 表示本地文件最后修改日期，`If-Modified-Since` 会将 `Last-Modified` 的值发送给服务器，询问服务器在该日期后资源是否有更新，有更新的话就会将新的资源发送回来。
但是如果在本地打开缓存文件，就会造成 Last-Modified

* ### ETag 和 If-None-Match
`ETag` 类似于文件指纹，`If-None-Match` 会将当前 ETag 发送给服务器，询问该资源 `ETag` 是否变动，有变动的话就将新的资源发送回来。并且 `ETag` 优先级比 `Last-Modified` 高。


