---
title: 在Euserv上部署GoneList并使用Argo tunnel
description: 如何折腾Euserv
date: 2021-02-22T14:14:41+09:00
image: cover.jpg
slug: gonelist-only-ipv6-argo
---
###### 186指导
如何安装Argo Tunnel可以参考 **[这里](https://blog.186526.xyz/post/argo-tunnel-for-free/)**。  

**上面的教程已经教你如何使用Cloudflared了，下面直入正题，安装[Gonelist](https://github.com/gonelist/gonelist/)**

#### 第一步
**在 [GitHub Release](https://github.com/cugxuan/gonelist/releases) 下载相应构架的压缩包**  

#### 第二步
**下载完成后解压出来后文件夹名就是gonelist_系统_构架**

#### 第三步
**比如我下载的是linux_amd64，下面就要输入`cd gonelist_linux_arm64`然后再输入`./gonelist_linux_amd64`Gonelist就会运行在8000端口**

#### 第四步
**可以使用nohup来守护进程，想结束进程可以使用`ps -ef | grep go`来查找进程号**

#### 进阶玩法
##### **使用systemd守护进程**
> 下载这个[脚本](https://raw.githubusercontent.com/gonelist/gonelist/master/scripts/install-release.sh)  
> 运行他 `bash install-release.sh -l gonelist_系统_构架.tar.gz`  
> 这样就能用systemd守护进程辣  
>> systemctl start gonelist  
>> systemctl stop gonelist  
>> systemctl status gonelist  
>>> ps.使用脚本安装后配置文件在`/etc/gonelist/`  

##### **配置config.json**
> 申请`client_id`和`client_secret`的教程一抓一大把就不说了。   
> 主要修改的就是`redirect_url`和`site_url`  
>> `redirect_url`修改为`http://yourdomain:8000/auth`  
>> `site_url`修改为`http://yourdomain:8000/`  

##### **世纪互联**
> 我没有世纪互联账号，所以我不确定能不能用。  
> 在`config.json`中有一段`china_cloud`  
> 将`enable`的值改为`true`  
> `client_id`和`client_secret`我也不说了  

### Argo Tunnel启动！
```console
cloudflared tunnel --hostname yourdomain.com --url localhost:8000 --name 自己写个名
```
# **可以用screen防止关闭ssh就白给的情况**