# content-type详解

> 截止到目前为止，我经常使用content-type的地方有三个：
> 1.postman
> 2.ajax
> 3.http 模块（nodejs）

一般来说，首先使用postman调试一下接口是否可用，然后再去写代码，接下来，会对比这3种情况以及4种常用的content-type类型。

**官方定义：**

```
http请求头
```

1. content-type:multipart/form-data

```
上传文件
```

2. content-type:application/x-www-form-urlencoded

```
一般请求
```

3. content-type:text/plain

boundary

