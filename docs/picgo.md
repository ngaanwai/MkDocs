---
title: picgo
tags: #vscode #picgo
---

# vscode picgo github jsdelivr 配置
# github新建一个仓库

新建一个仓库，填写好仓库名

仓库描述（可选）

将权限设置成 public 或 private

根据需求选择是否为仓库初始化一个 README.md 描述文件

# 生成token

点击头像-Settings -Developer settings-Personal access tokens-new
勾选了无限期-repo-generate
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

# 配置picgo

设定仓库名（Repo）：按照 用户名/图床仓库名 的格式填写

设定分支名（Branch）：main

设定 Token：粘贴之前生成的 Token

指定存储路径（Path）：填写想要储存的路径，如image/，所有通过插件上传的图片都在图床仓库中的image文件夹下（后面的/必须加上，不然image就是上传后的图片名前缀）

设定自定义域名（Custom Url）：它的的作用是，在图片上传后，PicGo 会按照自定义域名 上传的图片名的方式生成访问链接，放到粘贴板上，因为我们要使用 jsDelivr 加速访问，所以可以设置为：

https://cdn.jsdelivr.net/gh/用户名/图床仓库名  
or  
https://testingcf.jsdelivr.net/gh/用户名/图床仓库名

fastly.jsdelivr.net
gcore.jsdelivr.net
testingcf.jsdelivr.net

jsdelivr 将每个 CDN 都单独做了个子域名，在前段时间 jsdelivr 掉北岸故障的时候，官方还让大家 Ping 一下这些域名，看看哪个更快一些。

