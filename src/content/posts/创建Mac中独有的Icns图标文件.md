---
title: 创建Mac中独有的Icns文件
author: Francisco
description: .icns 文件是 macOS 的图标格式，包含多种尺寸的高分辨率图标。创建过程包括准备1024x1024图标、使用命令生成不同尺寸的图标文件，并最终生成.icns文件。
pubDate: 2025-4-12
categories: ["Mac"]
slug: icns-file-format
pin: false
---

Icns文件是 macOS 的图标文件格式，它是 Apple 的专有格式，通常包含多个尺寸的图标用于适应不同的显示需求。

准备一张1024 x 1024图标Image，我是使用Figma设计的自己的Icon直接导出。

通过命令创建不同尺寸的图标文件

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

使用命令创建icns文件

```bash
iconutil -c icns icons.iconset -o icon.icns
```
