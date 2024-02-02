---
title: nginx
tags: [computer]
---

# 配置文件

配置文件大致结构
location在nginx配置文件中的位置
```json
#user  nobody;
worker_processes  1;

#event块
events {
    worker_connections  1024;
}

http {
    #http全局块
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;
    #server块
    server {
        #server全局块
        listen       8000;
        server_name  localhost;
        #location块
        location / {
            root   html;
            index  index.html index.htm;
        }
    }
    #这边可以有多个server块
    server {
      ...
    }
}
```

## server
### listen
|配置|说明|
|---|---|
|listen 127.0.0.1:8000; | #只监听来自127.0.0.1这个IP，请求8000端口的请求  
|listen 127.0.0.1; |#只监听来自127.0.0.1这个IP，请求80端口的请求(不指定端口，默认80)  
|listen 8000;| #监听来自所有IP，请求8000端口的请求  
|listen *:8000;| #和上面效果一样  
|listen localhost:8000;| #和第一种效果一致

### sever_name
可以使用精确地址、通配符(*)或正则表达式,正则表达式以~开头.
```json
server {
    listen       80;
    server_name  example.org  www.example.org;
    ...
}
server {
    listen       80;
    server_name  *.example.*;
    ...
}
server {
    listen       80;
    server_name  ~^(?<user>.+)\.example\.net$;
    ...
}
```

### location
语法规则
```json
location [ = | ~ | ~* | ^~ ] uri { ... }
```

符号含义
|符号|含义|
|---|---|
|=|表示精确匹配。只有完全相等才能匹配上，比如location = /one/ 只有$server_name/one/才能匹配上，$server_name/one都无法匹配到|
|^~|以uri开头的就能匹配到，比如location ^~ /one 能够被$server_name/one匹配到，也能被$server_name/one/two匹配到
|~|区分大小写的正则匹配|
|~*|不区分大小写的正则匹配|
|/|通用匹配，任何请求都会匹配到|

如果uri包含正则表达式，就要使用“～”或者“～*”标识.  
nginx不对uri进行编码，因此经过浏览器编码过的请求为/static/20%/aa，可以被规则 ^~ /static/ /aa匹配到（注意是空格）

匹配顺序  
同一个 server 中有多个 location 配置的情况下的匹配顺序为：
-  首先匹配 =
-  其次匹配 ^~
-  其次是按文件中顺序的正则匹配
-  最后是交给 / 通用匹配
- 当匹配成功时候会立即停止匹配，按当前匹配规则的 location 来处理请求

比如将server_name根目录地址转发到特定uri
```json
    location = / {
      proxy_pass https://xxx/uri;
    }
```
root指令  
这个指令用于设置请求寻找资源的跟目录，此指令可以在http块、server块或者location块中配置。当我们访问服务器命中了 location 的配置时，nginx 的 location 会优先匹配到此代码块，会指向 location 中所配置的 root , server 中的 root 不会生效。

root和alias区别  
区别在于 nginx 如何解释 location 后面的 uri，这会使两者分别以不同的方式将请求映射到服务器文件上。
- root 的处理结果是：root路径 ＋ location路径
- alias 的处理结果是：使用 alias 路径替换 location 路径

比如django设置静态文件目录
```json
    location /static {
        alias /django/project_name/collected_static_dir;
    }
```