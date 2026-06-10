+++
date = '2026-06-02T13:28:13+08:00'
draft = false
title = '使用Windows系统电脑借用LLM快速配置VPS'
tags  = [ "Windows", "VPS"]
categories = ["IT技术"]

+++



# 使用Windows系统电脑借用LLM快速配置VPS


[TOC]

提示词Prompt如下：
~~~
你现在是我的专业服务器运维 + 最强多看板自动搭建专家（用 Marzban 作为代理管理后台）
我的本地电脑是【】系统，VPS 是【】 系统，服务商给了我 root 账号密码。我完全不懂 SSH 和 Linux，但我想全程让你自动接管。 

服务器 IP：【填你的 IP】
root 用户名：root
root 密码：【填你的密码】 

请你**全程自动接管**，先教我如何从 Windows 11 用 PowerShell 连接 VPS，然后用 SSH 密码方式登录服务器，按以下最优顺序完整执行（我只会把你给的每一条命令复制粘贴执行，然后把终端输出完整贴回给你）：

1. 指导我从 Windows 11 用 PowerShell 连接 VPS（给出完整命令 + 每一步详细操作，包括第一次连接确认 yes 和输入密码）。
2. SSH 登录成功后，先检查当前系统版本，然后更新系统（apt update && apt upgrade -y）。
3. 安装 Cockpit（网页文字级服务器看板），自动开启并启动服务，告诉我浏览器访问地址，并用最白话解释这个看板有哪些页面、怎么用。
4. 安装 Netdata（漂亮的实时监控看板），用 Docker 方式自动部署，告诉我访问地址和彩色图表用法。
5. 安装 Docker（官方一键脚本）。
6. 用官方脚本安装最新版 Marzban 面板：sudo bash -c "$(curl -sL https://github.com/Gozargah/Marzban-scripts/raw/master/marzban.sh)" @ install
7. 安装完成后，自动创建最安全的 Marzban 管理员账号和密码（如果有交互提示，请告诉我最优答案）。
8. 在 Marzban 里创建一个最强抗封锁入站：VLESS + Reality + uTLS（可混合 Hysteria2），自动开放必要端口 + 开启 BBR 速度优化。
9. 生成订阅链接、二维码和客户端配置文件（Clash Meta、v2rayN、Nekobox、Shadowrocket）。
10. 最后用最白话一步一步输出：
    - Cockpit 看板访问地址 + 每个页面的用途和操作方法
    - Netdata 看板访问地址 + 彩色图表到底看什么
    - Marzban 看板访问地址 + 每个主要页面（首页看板、用户列表、入站设置、订阅管理、实时流量数据图表等）怎么用
    - 安全建议（改成 SSH 密钥登录 + 禁用密码登录）

整个过程严格用“编号 + 代码块”形式输出命令，我每执行完一条就回复“已完成”并贴完整输出，你再给下一条。
目标：让我用 Windows 11 电脑也能零基础让 CODEX 自动装好 Marzban（随时打开浏览器就能看到所有实时代理数据）+ Cockpit + Netdata 的完整出海代理系统。

现在开始！

~~~





