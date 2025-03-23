---
weight: 100
title: "aibrix"
description: ""
icon: "article"
date: "2025-3-22T21:04:02+08:00"
lastmod: "2025-3-22T21:04:02+08:00"
draft: true
toc: true
---

windows 环境里如何安装 aibrix
1. 安装 wsl2
2. 安装 ubuntu
3. 打开 ubuntu，安装 podman
```shell
sudo apt install curl ca-certificates
sudo apt install podman
```
4. 安装 minikube 
```shell
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

5. 启动 minikube
```shell
minikube start --driver=docker --image-mirror-country='cn' --image-repository=registry.cn-hangzhou.aliyuncs.com/google_containers 
```

5. 如果出现 dns 劫持问题，需要设置 wsl 安装的系统使用宿主机 dns 配置，`vim /etc/wsl.conf` 增加如下内容
```shell
[network]
generateResolvConf = false
```
6. 重启 wsl2 所安装的系统
7. 手动设置 dns，`vim /etc/resolv.conf`
```shell
nameserver 8.8.8.8
nameserver 1.1.1.1
```
8. 验证 dns 解析是否正常
```shell
nslookup dl.k8s.io
```
9. 如果要设置代理环境，需要在 ~/.bashrc 增加如下配置
```shell
export http_proxy="http://127.0.0.1:1080"
export https_proxy="http://127.0.0.1:1080"
```

### 安装 gpu 驱动
1. 更新 apt sources 源
```shell
deb http://mirrors.aliyun.com/ubuntu/ noble main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ noble main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ noble-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ noble-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ noble-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ noble-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ noble-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ noble-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ noble-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ noble-backports main restricted universe multiverse
```
2. 