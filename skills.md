---
title: 服务与技巧
description: 一些实用技能/服务拾遗
published: true
date: 2026-01-25T15:07:37.359Z
tags: skills, services
editor: markdown
dateCreated: 2026-01-25T15:07:37.358Z
---

# 服务与技巧

## 信息服务

### 校园网

#### Wi-Fi/有线网认证指南

这里介绍关于[上海科技大学网络服务](https://it.shanghaitech.edu.cn/wlfw/list.htm)的认证配置。

- `ShanghaiTech`：上科大统一 WiFi，只在上科大内提供服务。
	- 账号：学号
	- 密码：统一身份认证密码（egate密码）
- `eduroam`：教育漫游 WiFi，可在所有 [有该网络的大学/机构](https://www.eduroam.org/where/) 按下列账号密码登录。
	- 账号：`学号@shanghaitech.edu.cn`
	- 密码：统一身份认证密码（egate密码）
- `ShanghaiTech-Guest`：上科大校内游客 WiFi，连接后通过**网页认证**
	- 账号：学号
	- 密码：统一身份认证密码（egate密码）
- 有线网认证：有线网认证，通过**网页认证**
	- 账号：学号
	- 密码：统一身份认证密码（egate密码）

**官方文档：**

- [无线网络接入指南](https://it.shanghaitech.edu.cn/2021/0423/c8423a63174/page.htm)
- [有线网络接入指南](https://it.shanghaitech.edu.cn/2021/0423/c8423a63173/page.htm)
- [无线 eduroam 接入指南](https://it.shanghaitech.edu.cn/2021/0423/c8423a63182/page.htm)

**FAQ:**

- **Linux 如何配置？**
	- Linux 大致类似 Android 配置，安全性选择 `WPA & WPA2 Enterprise`，认证方式选择 `PEAP`，PEAP 版本号自动，内部认证方式选择 `MSCHAPv2`。记得勾选无需 CA 证书，用户名和密码如上填写。
- **重新修改密码了怎么办**
	- 一般重新修改密码会关联到无线网络的密码修改，但相关延迟从数小时到几天不等，建议是**除非你的设备被强制下线，否则不要手动断开连接或忘记网络**。在特殊活动前记得提前修改密码，以免出现恰好无法登录无线服务的情况。

如有其他情况，请立刻拨打图书与信息中心 7x24 服务热线 `021-20685566`，或者电邮到 it-support@shanghaitech.edu.cn。

## 校园邮箱

### 邮箱客户端配置指南

在 https://mail.shanghaitech.edu.cn 最上方的 [帮助中心](https://mail.shanghaitech.edu.cn/coremail/help/index_zh_CN.jsp) 里可见详细的配置指南。

客户端配置参考 [此页面](https://mail.shanghaitech.edu.cn/coremail/help/clientoption_zh_CN.jsp)，值得一提的是，邮箱现在使用了多因素认证 + 客户端专属密码这一业界常用的方案来防止邮件被盗用。

你需要在 个人设置——安全设置——客户端专用密码 页面中生成专属密码，将他作为你的客户端填写的密码而不是邮箱密码。

### 邮箱使用第三方认证器

下面是一种不使用 Coremail APP，连接到第三方认证器的方法：

首先你需要配置多因素认证，通常情况下你需要使用备用邮箱、手机号以及下载软件来认证。为此，GeekPie 社团编写了 [ShanghaiTech-Mail-TOTP](https://github.com/ShanghaitechGeekPie/ShanghaiTech-Mail-TOTP?tab=readme-ov-file) 项目，当你安装了油猴插件时可以使用此插件，将 APP 认证改为普通的 TOTP 方式。从而让你能够导入到例如 Ageis，Google Authenticator 等软件中。

日后登录时只需要选择 CoreMail APP 验证码，填写你从认证器获取的 TOTP 代码即可。