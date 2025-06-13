---
title: Ubuntu 初始化
author: Francisco
description: Ubuntu Server 22.04 LTS的Zsh安装步骤，包括Oh-My-Zsh和Powerlevel10k主题的配置，以及Panel的安装和推荐命令如Neofetch、Htop和Duf的使用方法。
pubDate: 2023-2-12
categories: ["Ubuntu", "服务器"]
slug: ubuntu-initialization
pin: false
---

- **版本号**: Ubuntu Server 22.04 LTS 64bit
- **平台**: [腾讯云](https://cloud.tencent.com/)
- **参数**: 2核+4GB+70GiB+6Mbps
- **SSH工具**: [Tabby](https://tabby.sh/)
- **字体**: **JetBrainsMono Nerd Font** [Nerd Fonts](https://www.nerdfonts.com/)

# Zsh

## 1.安装 Zsh

- 更新本地软件包列表 `sudo apt update`
- 安装 Zsh `sudo apt install zsh`
- 检查 Zsh 版本号 `zsh --version`

## 2.安装 Oh-My-Zsh

- 下载脚本 `wget <https://gitee.com/mirrors/oh-my-zsh/raw/master/tools/install.sh>`
- 脚本添加可执行权限 `chmod +x install.sh`
- 运行脚本 `./install.sh`

## 3.安装 Powerlevel10k 主题和插件

### 下载主题

```bash
git clone --depth=1 <https://gitee.com/romkatv/powerlevel10k.git> ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

### 下载插件

```bash
# 进入plugins文件夹
cd ~/.oh-my-zsh/custom/plugins
# 下载插件
git clone <https://github.com/zsh-users/zsh-syntax-highlighting.git>
git clone <https://github.com/zsh-users/zsh-autosuggestions.git>
git clone <https://github.com/zsh-users/zsh-completions.git>
git clone <https://github.com/wting/autojump.git>
```

### 编辑配置文件

```bash
# 打开配置文件
vim ~/.zshrc
# 修改主题为powerlevel10k
ZSH_THEME="powerlevel10k/powerlevel10k"
# 添加插件
plugins=(git zsh-completions zsh-autosuggestions autojump zsh-syntax-highlighting)
# 重载zsh配置文件
source ~/.zshrc
```

## 疑问

- **Powerlevel10k初始化选项如何选?**

  无脑选Y, 挑选自己喜欢的选项就好

- **字体 Icon 显示不全?**

  下载安装Nerd字体解决 [Nerd Fonts](https://www.nerdfonts.com/)

# Panel

## 1.下载安装

```bash
curl -sSL <https://resource.fit2cloud.com/1panel/package/quick_start.sh> -o quick_start.sh && sudo bash quick_start.sh
```

## 2.安装流程

- **开始安装 (安装根目录输入”/”)**

![](https://s2.loli.net/2025/06/12/7TQAzmgLWZf5lsd.png)

- **面板端口号 (可默认 | 可自定义)**

![](https://s2.loli.net/2025/06/12/GSjl3nadufLKXw5.png)

- **用户名 | 密码 (可默认 | 可自定义)**

![](https://s2.loli.net/2025/06/12/HTnoAJ9kxd5rPuw.png)

- **访问登录 (访问外网网址)**

![](https://s2.loli.net/2025/06/12/cW8xSrfBX3jZURI.png)

## 3.账号密码登录

![](https://s2.loli.net/2025/06/12/6ZQj9nEcFh1AbIp.png)

## 4.登录成功

![](https://s2.loli.net/2025/06/12/VWkt8C3cyFTrf5Y.png)

# 推荐命令

## Neofetch(系统信息)

**开源地址**

[GitHub - dylanaraps/neofetch: 🖼️ A command-line system information tool written in bash 3.2+](https://github.com/dylanaraps/neofetch)

**安装**

- `sudo apt install neofetch`

**演示**

![](https://s2.loli.net/2025/06/12/wG8lLFAeyija5VB.png)

## Htop(进程监控工具)

**开源地址**

[GitHub - htop-dev/htop: htop - an interactive process viewer](https://github.com/htop-dev/htop)

**安装**

- `sudo apt install htop`

**演示**

![](https://s2.loli.net/2025/06/12/jlNH3bIqiywAPe1.png)

## Duf(磁盘使用情况)

**开源地址**

[GitHub - muesli/duf: Disk Usage/Free Utility - a better ‘df’ alternative](https://github.com/muesli/duf)

**安装**

- `sudo apt install duf`

**演示**

![](https://s2.loli.net/2025/06/12/U98Sm6ZcEqHP4hw.png)

## Exa(文件列表查看)

**开源地址**

[GitHub - ogham/exa: A modern replacement for ‘ls’.](https://github.com/ogham/exa)

**安装**

- `sudo apt install exa`

**演示**

![](https://s2.loli.net/2025/06/12/IE4yTf79BDWoRX2.png)
