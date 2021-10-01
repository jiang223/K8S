---
description: 安装docker以及k8s软件踩坑集锦，本章节将简要讲述如何在win10安装云原生的基础环境(docker k8s)以及注意事项。
---

# Envirenment Ready

## 一、Docker软件安装

### 1、开启win10虚拟机

win10系统自带Hyper-V，百度搜索Hyper-V即可使用开启，这一步较简单

### 2、安装docker软件

{% embed url="https://hub.docker.com/editions/community/docker-ce-desktop-windows" %}

傻瓜式点击安装，百度一堆

## 二、在Docker中安装K8S

{% embed url="https://github.com/AliyunContainerService/k8s-for-docker-desktop" %}

按上述链接操作。

注意这个安装可能需要重复尝试的，按照github上拉取的只是部分的镜像，后在docker开启k8s后，还会从服务上拉取缺失的镜像，这一步需要配置可用的docker镜像仓库，如果等待时间超过30分钟，需要resert docker环境后，再换个仓库从新弄。本人昨天弄了一下午才好。

至此，win10云原生基本环境算是搭建完毕

