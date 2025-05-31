# Sing-box 配置文件教程

本项目收集了 sing-box 的常用配置文件，适用于 AnyTLS、ChatGPT 代理、Reality 协议等多种场景。适合新手快速上手和进阶用户参考。

## 目录结构

- `AnyTLS/`：TLS 相关配置（客户端/服务端）
- `ChatGPT/`：ChatGPT 代理配置（客户端/服务端，含不同版本）
- `reality/`：Reality 协议配置（客户端/服务端，含不同版本）

---

## 一、Sing-box 安装方法

### 1. 官方安装（推荐）

前往 [sing-box 官方发布页](https://github.com/SagerNet/sing-box/releases) 下载适合你系统的预编译包，解压后即可使用。

### 2. Linux 一键安装（以 x86_64 为例）

```bash
wget https://github.com/SagerNet/sing-box/releases/latest/download/sing-box-linux-amd64.tar.gz
tar -xzvf sing-box-linux-amd64.tar.gz
cd sing-box-*
sudo mv sing-box /usr/local/bin/
sing-box version
```

### 3. 其他平台

请参考 [官方文档](https://sing-box.sagernet.org/zh/installation/)。

---

## 二、配置文件说明

### 1. AnyTLS（TLS 相关配置）

- `client-config-anytls-1.12.0(Android).json`  
  适用于 Android 客户端，包含 DNS、入站（tun/mixed）、出站（anytls、直连）、路由等详细配置。  
  **主要字段说明：**
  - `dns`：自定义 DNS 服务器及规则，防止 DNS 污染。
  - `inbounds`：tun 适配器用于透明代理，mixed 支持多协议。
  - `outbounds`：anytls 用于加密代理，direct 直连，selector/urltest 实现自动切换。
  - `route`：根据域名/IP/协议自动分流，广告拦截、国内外分流等。
  - `tls`：详细的 TLS 配置，支持 Reality。

- `server-config-anytls-1.12.0.json`  
  适用于服务端，监听 443 端口，支持 Reality，详细的 padding、TLS、用户认证等配置。

### 2. ChatGPT（ChatGPT 代理配置）

- `1.12.0/chatgpt-client-1.12.0 (Android).json`  
  适用于 Android 客户端，专为 ChatGPT/OpenAI 代理优化，自动分流 OpenAI 流量，支持 Reality 协议。

- `1.12.0/chatgpt-server-1.12.0.json`  
  服务端配置，支持 VLESS + Reality，内置 WireGuard（warp）出站，自动分流 OpenAI/Abema 流量。

**注：不同版本文件夹（如 1.10.0、1.11.0）为不同 sing-box 版本适配，选择与你客户端/服务端版本一致的配置。**

### 3. reality（Reality 协议配置）

- `1.12.0/client-config-vless-reality-1.12.0(Android).json`  
  适用于 Android 客户端，VLESS + Reality 协议，详细分流规则，支持自动切换。

- `1.12.0/server-config-vless-reality-1.12.0.json`  
  服务端配置，监听 443 端口，Reality 协议，详细用户与 TLS 配置。

---

## 三、使用方法

1. **选择合适的配置文件**  
   根据你的系统（Android/Linux）、用途（客户端/服务端）、协议（AnyTLS/Reality/ChatGPT）选择对应的配置文件。

2. **修改必要参数**  
   - 服务端地址、端口、UUID/password、public_key/short_id 等需与你的服务端实际信息一致。
   - DNS、路由规则可根据需求自定义。

3. **运行 sing-box**  
   ```bash
   sing-box run -c /path/to/your-config.json
   ```

4. **客户端建议**  
   - Android 推荐使用 [SagerNet](https://github.com/SagerNet/SagerNet) 或 [sing-box Android](https://github.com/SagerNet/sing-box-android)。
   - Windows/Mac/Linux 可直接用官方二进制。

---

## 四、常见问题与建议

- **配置报错？**  
  请用 `sing-box check -c your-config.json` 检查配置文件格式。
- **Reality 连接失败？**  
  检查 public_key、short_id、server_name 是否与服务端一致，端口是否开放。
- **分流不生效？**  
  检查 route/rule_set 配置，确保规则文件可正常下载。
- **更多问题**  
  请参考 [sing-box 官方文档](https://sing-box.sagernet.org/zh/) 或提交 issue。

---

## 五、贡献

欢迎提交 PR 或 issue，完善更多配置和教程！

---

> 本项目仅供学习与交流，请勿用于非法用途。
