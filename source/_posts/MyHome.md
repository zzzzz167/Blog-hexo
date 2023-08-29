---
title: 浅谈我家的服务及实现
date: 2023-08-29 13:55:59
tags: 
  - Network
  - Docker
  - HomeProject
index_img: /img/post_banner/MyHome/banner.png
banner_img: /img/post_banner/MyHome/banner.png
---


简单的记录下自家的目前服务和解决方案

<!---more-->

概况:

1. 面积, 整个房子共上下两层.
2. 强电, 强电部分上下各一个配电箱.
3. 弱电, 弱电部分全部汇总到二楼的弱电箱.

## 基础网络 拓扑

概况: 每个屋子均有预留网络, 墙内铺设超五类网线, 客厅留有 2 个网口, 且不使用 IPTV.

### 硬件

1. 主路由: 小米的 AX6000
2. 接入点(也是路由): TP-LINK 的 TL-WDR5620✖️3
3. 交换机: TPLINK 的 TL-SG2008D

### 拓扑

![拓扑图](网络拓扑图.png)

其中光猫为桥接模式, 由 AX6000 拨号 + DHCP服务器, 其余路由器作为接入点使用(有线 AP),IP 池从 234 开始倒序分配.

*因为没有 mesh 的路由器所以全是手动配置的呃呃呃呃

## 服务提供

全屋的服务主要是影音娱乐(吃 GPU 与 CPU 能力) 和不间断服务(需要长时间不关机 不吃 U 能力)

大部分包使用 docker 进行部署

### 硬件

1. 不间断服务提供: raspberr-pi 4 [4GB+32GB(SD)+512GB(机械)]
2. 影音: XPS15 (12 核 8GB+512GB(SSD)+1TB(机械))
3. 传感器: ESP8266

### 软件

#### Docker

项目地址: <https://www.docker.com/>

安装位置: XPS15 & raspberry-pi

方便项目部署的肯定得有, 要不然环境装这么多东西肯定很乱.

#### Rsync

项目地址: <https://github.com/WayneD/rsync>

安装位置: XPS15 & raspberry-pi & 我自己电脑

用来局域网大文件互传, 在后面上传电视剧, 电影的时候巨好用

#### CasaOS

![CasaOS](casaos.jpg)

项目地址: <https://github.com/IceWhaleTech/CasaOS>

安装位置: raspberry-pi

这个就是一个 docker + 系统的 web 可视化管理, 有自己的 App Store也自带了一些 docker 的镜像一键安装, 但是版本都比较老, 我一般都是自己填参数什么的, 有 SMB 功能, 可以简单的当做云盘使用, 稍微有点点鸡肋但是界面挺现代化.

安装的话有一建安装脚本, 挺方便的

#### Flare

![Flare](flare.jpg)

项目地址: <https://github.com/soulteary/docker-flare>

安装位置: docker + raspberry-pi

轻量、快速的个人导航页面, 因为服务太多啦, 我用它来导航记录我各个服务的地址,无任何数据库依赖, 巨好用٩(•̤̀ᵕ•̤́๑)ᵒᵏᵎᵎᵎᵎ.

#### HomeAssistant

![HomeAssistant](homeassiant.jpg)

项目地址: <https://www.home-assistant.io/>

安装位置: docker(host) + raspberry-pi

最流行的家庭助理了算是, 能帮你接入各种平台的智能家具, 同时也有很大的扩展能力.

##### HACS

项目地址: <https://github.com/hacs>

Homeassiant 的扩展商店能让你找到各种奇奇怪怪的插件和主题.

#### memos

![memos](memos.png)

项目地址: <https://usememos.com/>

安装位置: docker + raspberry-pi

一个很轻量并且美观有很多功能的记事本软件, 使用 md 的语法, 能让我全神贯注的记录和快捷的搜索我的想法,

#### Calibre-Web

![Calibre](Calibre.png)

项目地址: <https://github.com/janeczku/calibre-web>

镜像标签: johngong/calibre-web:latest

安装位置: docker + raspberry-pi

书库, 能自动从豆瓣等网站获取书籍信息, 后端是 py 的, 反应上来说稍微慢点但是好用, 我用来存漫画和小说还有一些项目的 pdf 文档.

#### n8n

![n8n](n8n.png)

项目地址: <https://docs.n8n.io/>

安装位置: docker + raspberry-pi

一个简单的自动化, 是那种类似 node-red 的自动化, 但是这个更适合家用, 因为比较简单且带着各种常用的模块, 我一般用它自动给手机推送我关注的博客的 RSS 和每日的新闻.

#### Grafana

![Grafana](Grafana.png)

项目地址: <https://grafana.com/>

安装位置: docker + raspberry-pi

用来监视家里服务器的运行状态和各个机子上 docker 的情况, 应该是有更厉害的用法, 目前没研究, 是一个可以高度自定义的监控面板.

#### prometheus

项目地址: <https://prometheus.io/>

安装位置: docker + raspberry

高性能时序数据库, 用来当我监视东西的后端数据库.

##### node_exporter

安装位置: XPS15 & raspberry-pi

提供电脑监视原数据

#### jellyfin

![jellyfin](jellyfin.png)

项目地址: <https://jellyfin.org/>

安装位置: docker + XPS15

作为本地的流媒体提供软件, 上面我用来存电视剧, 动漫等, 支持多客户端, DLAN 什么的, 很方便, 算是我家的家庭影音中心

##### nvidia-container-toolkit

项目地址: <https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html>

安装位置: xps15 作为 docker 扩展

方便我 n 卡对视频进行硬件解码.

#### immich

![immich](immich.png)

项目地址: <https://github.com/immich-app/immich>

安装位置: docker + XPS15

作为我们家的家庭相册的云盘, 保存到云端, 来减缓手机压力与家人共享什么的

## 未来设想

搞个 open-wrt 做软路由在主路由旁当旁臂路由来作为家里的代理服务器.

音乐播放器, 这个马上就要整了.
