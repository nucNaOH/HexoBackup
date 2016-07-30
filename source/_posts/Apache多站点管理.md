---
title: Apache多站点管理
date: 2016-07-13 19:37:32
categories: [配置]
tags: Apache
---

### 修改文件:apache/conftpd.ctf
#### 找到这两句取消注释

<!-- more -->
``` bash
#LoadModule vhost_alias_module modules/mod_vhost_alias.so
#Include conf/extratpd-vhosts.conf   
```

### 在DocumentRoot下添加：
``` XML
<Directory "F:/php">
    Options Indexes FollowSymLinks Includes ExecCGI   
    AllowOverride All   
    Require all granted
</Directory>
```

### 修改文件：apache/conf/extratpd-vhosts.conf
#### 添加以下内容

``` XML
<VirtualHost *:80>
    DocumentRoot "F:/php"   
	ServerName www.zhangziye.com
</VirtualHost>
```

### 修改C:/windows/system32/drivers/detc/hosts
#### 添加：

> 127.0.0.1       www.zhangziye.com##注意前面不要加#号

