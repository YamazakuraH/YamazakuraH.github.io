---
title: 如何搭建一个Onemanager
description: 使用OpenResty
date: 2021-02-22T12:45:34+09:00
image: cover.jpg
slug: create-onemanager
categories: 技术
---

### OS：Debian10

#### 咱打算直接照抄186的Onemanager-Flyio

**啥也不说了，直接进入主题。**
```console
sudo apt-get update
```
**安装需要的程序**
```console
sudo apt-get install --no-install-recommends ca-certificates gnupg2 gettext-base lsb-base lsb-release software-properties-common wget -y
```
**安装openresty**
```console
wget -O - https://openresty.org/package/pubkey.gpg | sudo apt-key add -
```
```console
sudo add-apt-repository -y "deb http://openresty.org/package/debian $(lsb_release -sc) openresty" 
```
```console
sudo apt-get update
```
```console
sudo apt-get install --no-install-recommends openresty -y
```
**安装Php**
```console
sudo apt-get install --no-install-recommends php-bcmath php-curl php-cli php-fpm  php-gd php-json php-mbstring php-mysql php-pdo php-pear php-xml php-zip -y
```
```console
mkdir /run/php/
```
**下载Onemanager**
```console
wget https://git.qvqaq.ml/186526/OneManager-php/archive/master.tar.gz -P /www/
```
```console
cd /www/ && tar xvf master.tar.gz && rm -rf master.tar.gz && chmod -R 777 onemanager-php
```
**配置openresty**  
```
将 /usr/local/openresty/nginx/conf/nginx.conf 中的server段注释掉  
gzip on; 取消注释  
在 gzip on; 下面添加`include /etc/nginx/conf.d/*.conf;`
在 /etc/nginx/conf.d/ 下创建网站conf  
如果出现502错误尝试在 /usr/local/openresty/nginx/conf/nginx.conf 中修改 user （方法不止一种，这只是最简单的一个。）
```