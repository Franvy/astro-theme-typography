---
title: 当npx创建项目报错
author: Francisco
description: 使用npx命令创建Nuxt项目时遇到DNS污染错误，解决方法是查询最新IP地址并在本地Host文件中配置。推荐使用Cloudflare等DNS服务商。
pubDate: 2023-4-12
categories: ["DNS", "IP配置", "Nuxt", "前端"]
slug: npx-error-creating-nuxt-project
pin: false
---

## 问题

今天想创建一个Nuxt项目练练手，便使用npx命令创建项目

```bash
npx nuxi@latest init lucky
```

但在使用npx命令创建项目的时候报错。

```bash
ERROR Error:Failed to downLoad template from registry: fetch failed
```

后来查询问题的时候得知是属于“DNS污染”， 也就是DNS 服务商的电话簿对不上了。

- DNS 是互联网的“电话簿”，把域名（如 example.com）翻译成 IP 地址。
- DNS 污染通常发生在 DNS 查询的过程中：
  - 拦截请求，伪造响应。
  - 把错误的 IP 存入 DNS 缓存。
  - 接下来即使请求的是正确的域名，也返回错误的地址。

不同地区的DNS多多少少在不同的网站都会出现这样的问题，既然网络服务商无法及时解决这些个别问题，那我们就自己找最新的IP地址自己指向服务器或者使用其他家DNS服务商（Cloudflare（1.1.1.1））。

## 解决方案

首先登录**ipaddress**网站查询问题域名的最新IP地址：[https://www.ipaddress.com](https://www.ipaddress.com/)

![](https://s2.loli.net/2025/06/12/PV8Bs6zhL7gfGK5.png)

随后将最新IP地址配置在自己本地的Host中即可

![](https://s2.loli.net/2025/06/12/cGXFZj7zWfNV1PE.png)

附：macOS / Windwos Host文件目录

```bash
# macOS
/etc/hosts
# Windwos
C:\Windows\System32\drivers\etc\hosts
```
