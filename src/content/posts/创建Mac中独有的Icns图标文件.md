---
title: 创建Mac中独有的Icns文件
author: Francisco
description: .icns 文件是 macOS 的图标格式，包含多种尺寸的高分辨率图标。创建过程包括准备1024x1024图标、使用命令生成不同尺寸的图标文件，并最终生成.icns文件。
pubDate: 2025-4-12
categories: ["Mac", "Icon"]
slug: icns-file-format
pin: false
---

## 什么是icns

.icns 文件是 **macOS 的图标文件格式**，专门用于为 macOS 应用程序、文件、文件夹等提供高分辨率图标（支持 Retina）。它是 Apple 的专有格式，通常包含多个尺寸的图标（16x16、32x32、128x128、256x256、512x512、1024x1024 等），用于适应不同的显示需求。

## 如何创建

> 最终结构
> ├── icon.icns
> ├── icon.png
> └── icons.iconset
> ├── icon_128x128.png
> ├── icon_128x128@2x.png
> ├── icon_16x16.png
> ├── icon_16x16@2x.png
> ├── icon_256x256.png
> ├── icon_256x256@2x.png
> ├── icon_32x32.png
> ├── icon_32x32@2x.png
> ├── icon_512x512.png
> └── icon_512x512@2x.png

### 1.准备一张1024✖️1024图标Image

> 我是使用Figma设计的自己的Icon直接导出

![CleanShot 2025-06-13 at 12.53.21@2x](https://s2.loli.net/2025/06/13/dPGkJQE7DNR5Cqt.webp)![CleanShot 2025-06-13 at 12.56.28@2x](https://s2.loli.net/2025/06/13/VPQLJjUHN59eDau.webp)

### 2.通过命令创建不同尺寸的图标文件

创建文件夹

```bash
mkdir icons.iconset
```

命令创建多个不同尺寸图片

```bash
sips -z 16 16 icon.png -o icons.iconset/icon_16x16.png
sips -z 32 32 icon.png -o icons.iconset/icon_16x16@2x.png
sips -z 32 32 icon.png -o icons.iconset/icon_32x32.png
sips -z 64 64 icon.png -o icons.iconset/icon_32x32@2x.png
sips -z 128 128 icon.png -o icons.iconset/icon_128x128.png
sips -z 256 256 icon.png -o icons.iconset/icon_128x128@2x.png
sips -z 256 256 icon.png -o icons.iconset/icon_256x256.png
sips -z 512 512 icon.png -o icons.iconset/icon_256x256@2x.png
sips -z 512 512 icon.png -o icons.iconset/icon_512x512.png
sips -z 1024 1024 icon.png -o icons.iconset/icon_512x512@2x.png
```

![](https://s2.loli.net/2025/06/13/PEuZHsSa7ckFGd9.webp)

### 3.使用命令创建icns文件

```bash
iconutil -c icns icons.iconset -o icon.icns
```
