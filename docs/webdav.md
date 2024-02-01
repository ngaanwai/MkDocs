---
title: webdav
tags: #webdav
---
# webdav在windows注册表优化
从Windows Vista起，微软就禁用了http形式的基本WebDAV验证形式（KB841215），必须使用https连接。我们可以修改注册表……
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
找到BasicAuthLevel把这个值从1改为2，然后进控制面板，服务，把WebClient服务重启（没有启动的就启动它）。

在某些版本的 Windows 操作系统中，WebDAV 驱动器的最大文件大小被限制为 50MB。如果你试图复制超过 50MB 大小的文件，Windows 就会弹出错误提示框。当然，这个限制是可以通过修改注册表来消除的。

将注册表中位于
HKLM\SYSTEM\CurrentControlSet\Services\WebClient\Parameters\FileSizeLimitInBytes
处的键值由 50000000 (50MB) 修改为更大的数值。最大修改为：4294967295（0xffffffff）字节，即4G。
