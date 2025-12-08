<h1 align="center">🛰️ Linux 服务器外网代理配置（SSH + Clash 端口转发方案）</h1>

<p align="center">
  <i> —— 2025.12.8</i>
</p>



<p align="center">
  <img src="https://img.shields.io/badge/SSH-Remote%20Forwarding-blue?style=flat-square" />
  <img src="https://img.shields.io/badge/Platform-Linux-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Proxy-Clash-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Status-Complete-brightgreen?style=flat-square" />
</p>

---

本仓库记录了一套 **无需在服务器安装任何代理软件**、即可让服务器访问外网资源（如 GitHub、PyPI、Docker Hub 等）的解决方案。

核心思路是使用：

> **SSH -R 远程端口转发 + 本地 Clash 代理**  
> 使服务器的所有网络请求转发到你本地的代理上，实现稳定、可控的外网访问。

适用于：  
✔ git clone 超时  
✔ pip / conda 超时  
✔ curl / wget 无法访问 HTTPS  
✔ Linux 服务器完全无代理权限（无法安装代理客户端）

---

## 📦 Environment Overview

| 项目 | 内容 |
|----|------|
| 本地设备 | Windows / macOS 均可（需运行 Clash for Windows / ClashX） |
| 服务器 | Linux 系统，具有 SSH 登录权限 |
| 代理方式 | Socks5 via Clash |
| 核心原理 | SSH 远程端口转发 `-R` |

---

# 🔧 Step 1：确认本地 Clash 的代理端口

打开 **Clash for Windows / ClashX**，进入：

**Settings → General → 代理端口（Proxy Ports）**

一般配置如下：

| 类型 | 默认端口 |
|------|---------|
| HTTP Proxy | `127.0.0.1:7890` |
| Socks Proxy | `127.0.0.1:7891` 或 `7890` |

👉 **推荐使用 Socks 端口（例如 7890）**

如果你本地的 Socks 端口不是 7890，请在后续命令中替换成你自己的端口。

---
