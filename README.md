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

# 🔧 Step 1：确认本地 Clash 的代理端口

打开 **Clash for Windows / Clash Verge 等相关代理软件**，进入：

**Settings → General → Proxy Ports**

默认配置如下：

| 代理软件 | 默认端口 |
|------|---------|
| Clash for Windows | `127.0.0.1:7890` |
| Clash Verge | `127.0.0.1:7897` |

# 🔗 Step 2：本地 Session 建立 SSH 远程端口转发

```bash
ssh -R 1080:127.0.0.1:7890 username@server_ip
```

236机子直接copy
```bash
ssh -R 1080:127.0.0.1:7890 amax@192.168.208.236
```

# 🛠 Step 3：在服务器 Session 设置代理

方式 A：仅 git 使用代理
```bash
git config --global http.proxy  "socks5h://127.0.0.1:1080"
git config --global https.proxy "socks5h://127.0.0.1:1080"
```

方式 B：让所有程序走代理
```bash
export http_proxy="socks5h://127.0.0.1:1080"
export https_proxy="socks5h://127.0.0.1:1080"
export ALL_PROXY="socks5h://127.0.0.1:1080"
```


