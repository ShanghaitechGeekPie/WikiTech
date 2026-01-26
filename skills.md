---
title: 服务与技巧
description: 一些实用技能/服务拾遗
published: true
date: 2026-01-26T01:43:15.781Z
tags: skills, services
editor: markdown
dateCreated: 2026-01-25T15:07:37.358Z
---

# 服务与技巧

## 网络服务

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

### 返校 VPN

#### 使用 ATrust 客户端（手机/Windows/MacOS/部分 Linux）

具体参阅图信的 [电子资源校外访问](https://library.shanghaitech.edu.cn/4032/list.htm) 指南和附件 [20250107-上海科技大学校园VPN接入使用指南.pdf](https://library.shanghaitech.edu.cn/_upload/article/files/e1/cd/e09fb90d42129fbcee06bfe7ffc6/f6ee0aa5-8ef9-4e94-bd09-d24168fd6026.pdf)

#### 使用 Docker

由于 ATrust ~~过于流氓~~ 我们这里介绍一种使用 VPN 的方法，感谢开源项目 `hagb/docker-atrust`

Linux 等使用以下命令

```bash
sudo docker run --rm --device /dev/net/tun --cap-add NET_ADMIN -ti -e PASSWORD=88888888 -e URLWIN=1 -v $HOME/.atrust-data:/root -p 127.0.0.1:5901:5901 -p 127.0.0.1:1080:1080 -p 127.0.0.1:8888:8888 -p 127.0.0.1:54631:54631 --sysctl net.ipv4.conf.default.route_localnet=1 docker.1ms.run/hagb/docker-atrust
```

接下来使用任意 VNC 客户端连接到 `127.0.0.1:5901` 密码为上述命令里提供的 `88888888`

然后输入服务器地址 `vpn.shanghaitech.edu.cn`，点击连接

此时会出现两种情况：

- 你顺利的拿到了链接，点击复制，在你宿主机（非 VNC 内）访问这个地址并登录，完成
- 你没有拿到，有可能是因为弹出了强制更新等，那么请：
	- 直接在外部访问 [这个链接](https://ids.shanghaitech.edu.cn/authserver/login?service=https%3A%2F%2Fvpn.shanghaitech.edu.cn%3A443%2Fpassport%2Fv1%2Fauth%2Fcas)
  - 登录，一样可以完成
  
之后，你可以使用代理等工具，将 `http://172.0.0.1:8888` 或者 `socks5://127.0.0.1:1080` 作为你的代理地址。

## 校园邮箱

### 邮箱客户端配置指南

在 https://mail.shanghaitech.edu.cn 最上方的 [帮助中心](https://mail.shanghaitech.edu.cn/coremail/help/index_zh_CN.jsp) 里可见详细的配置指南。

客户端配置参考 [此页面](https://mail.shanghaitech.edu.cn/coremail/help/clientoption_zh_CN.jsp)，值得一提的是，邮箱现在使用了多因素认证 + 客户端专属密码这一业界常用的方案来防止邮件被盗用。

你需要在 个人设置——安全设置——客户端专用密码 页面中生成专属密码，将他作为你的客户端填写的密码而不是邮箱密码。

### 邮箱使用第三方认证器

下面是一种不使用 Coremail APP，连接到第三方认证器的方法：

首先你需要配置多因素认证，通常情况下你需要使用备用邮箱、手机号以及下载软件来认证。为此，GeekPie 社团编写了 [ShanghaiTech-Mail-TOTP](https://github.com/ShanghaitechGeekPie/ShanghaiTech-Mail-TOTP?tab=readme-ov-file) 项目，当你安装了油猴插件时可以使用此插件，将 APP 认证改为普通的 TOTP 方式。从而让你能够导入到例如 Ageis，Google Authenticator 等软件中。

日后登录时只需要选择 CoreMail APP 验证码，填写你从认证器获取的 TOTP 代码即可。

## 正版软件

学校为在校师生购买了多种正版软件授权，可通过 [软件管理服务平台-软件清单](https://software.shanghaitech.edu.cn/#/soft) 页面下载。

## 自助文印服务

学校在图书馆（如 1F 104 室）、教学区、宿舍楼等公共区域设有自助文印一体机，支持打印、复印和扫描服务。

### 收费标准

| 纸张规格 | 颜色 | 复印/打印 | 扫描 |
| :--- | :--- | :--- | :--- |
| **A4** | 黑白 | 0.08 元/页 | **免费** |
| **A4** | 彩色 | 0.6 元/页 | **免费** |
| **A3** | 黑白 | 0.16 元/页 | **免费** |
| **A3** | 彩色 | 1.2 元/页 | **免费** |

### 准备工作

在使用自助文印前，需要先完成**身份注册**并安装客户端。

#### 1. 身份注册
- **PC 端注册（推荐）**：连接校内网，打开“易安 (esafe) 自助打印复印系统 - 学生端”，点击“注册”，输入服务器 `print.shanghaitech.edu.cn`、学号/工号、姓名及自定义密码。
- **一体机端注册**：在文印机操作面板点击“注册”，按提示输入学号和密码。

#### 2. 驱动与客户端下载
- **下载地址**：[软件管理服务平台 - 自助文印系统](https://software.shanghaitech.edu.cn/#/softdetail?id=83)（仅限校内网访问）。
- **服务器地址**：`print.shanghaitech.edu.cn`。
- **配置提醒**：若安装后无法连接，请检查 `C:\SpoolPrintJob` 文件夹并确保你有访问/读写权限。

### 操作流程

#### 自助打印
1. **提交任务**：在 PC 上登录客户端，打开文档并选择打印，打印机选择 **`FonYuanXPSPrinter`**。
2. **刷卡登录**：前往任意一台自助一体机，将校园卡放置在刷卡区（**务必保留直到扣费结束**）。
3. **输出文档**：点击屏幕上的“打印”，选择你的任务并确认。
4. **扣费退出**：等待扣费成功提示后，取回校园卡。

#### 自助复印
1. **刷卡登录**：放卡。
2. **选择复印**：在屏幕选择复印功能，调整参数。
3. **完成退出**：取走文稿，取回卡。

#### 自助扫描
1. **插入 U 盘**：建议容量不超过 8GB。
2. **刷卡操作**：在屏幕选择扫描功能，通常路径为“扫描到外部记忆体”。
3. **获取文件**：完成扫描后取走 U 盘和校园卡。扫描服务目前**免费**。

> **⚠️ 注意事项**
> - **千万不要忘记取卡**：离开前请务必点击屏幕上的“返回”或“退出”，确保账户已登出，防止余额被盗刷。
> - **卡放稳**：由于结算是在取卡时进行的，打印过程中请勿移动校园卡。
> - **报修/咨询**：如遇卡纸或扣费异常，可联系图信中心工作人员（Tel: 021-20684836）。
{.is-warning}
