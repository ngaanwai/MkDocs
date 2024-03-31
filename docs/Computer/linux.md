---
title: linux
tags: [computer]
---
# linux常见问题及解决方案
## ssh
### 出现错误
例如：
WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED！
Host key verification failed.

You can either edit that text file manually and remove the old key (you can see the line number in the error message), or use
```
ssh-keygen -R 34.124.248.193
```

## firewalld
### 查看状态
```
sudo systemctl status firewalld
```
关闭
```
sudo systemctl stop firewalld
```
开启
```
sudo systemctl start firewalld
```

## selinux

### 查看状态
```
getenforce
```
或
```
sestatus
```

### 临时关闭
跟永久关闭中selinux的值改成permissive效果一样
```
sudo setenforce 0
```

### 永久关闭
#### 打开配置文件
```
sudo vim /etc/selinux/config
```
###### 将selinux的值改为disabled或permissive
```
SELINUX=permissive
```
###### 重启


### SELinux配置将httpd网络连接关闭导致的502错误
可以临时将selinux关闭，也可以设置httpd网络连接
#### 查看状态

```
getsebool httpd_can_network_connect
```
如果显示 httpd_can_network_connect --> off 则httpd网络连接关闭

#### 开启httpd网络连接

```
sudo setsebool -P httpd_can_network_connect 1
```
