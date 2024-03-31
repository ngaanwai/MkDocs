---
title: macos
tags: [computer]
---

# macos终端设置代理
## 临时使用代理（仅针对当前打开的Terminal窗口）
```
export http_proxy="socks5://192.168.50.239:1082" 
export https_proxy="socks5://192.168.50.239:1082" 
export all_proxy="socks5://192.168.50.239:1082"
```
## 永久代理设置
打开文件  
```
vi ~/.zshrc
```

修改内容  
```
alias proxy='export all_proxy=socks5://127.0.0.1:10808'
alias unproxy='unset all_proxy'
```
使配置生效  
```
source ~/.zshrc
```
### 测试
未开启代理下查询ip  
```
curl ipinfo.io
```
开启代理  
```
proxy
```
再次查询ip  
```
curl ipinfo.io
```
### 如需关闭代理，执行以下命令
```
unproxy
```