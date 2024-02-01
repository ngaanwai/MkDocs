---
title: macos终端设置代理
tags: #macos #terminal #proxy
---


## 临时使用代理（仅针对当前打开的Terminal窗口）

export http_proxy="socks5://192.168.50.239:1082" 
export https_proxy="socks5://192.168.50.239:1082" 
export all_proxy="socks5://192.168.50.239:1082"

## 永久代理设置

-   打开文件

```
vi ~/.zshrc
```

-   修改内容

```
alias proxy='export all_proxy=socks5://127.0.0.1:10808'
alias unproxy='unset all_proxy'
```

-   使配置生效

```
source ~/.zshrc
```

### 测试

```
curl ipinfo.io
```

```
{
  "ip": "122.238.62.243",
  "city": "Jiaxing",
  "region": "Zhejiang",
  "country": "CN",
  "loc": "30.7522,120.7500",
  "org": "AS4134 CHINANET-BACKBONE",
  "timezone": "Asia/Shanghai",
  "readme": "https://ipinfo.io/missingauth"
}%
```

```
proxy
```

```
curl ipinfo.io
```

### 如需关闭代理，执行以下命令

```
unproxy
```