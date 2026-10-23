# ⚡ CF Sub Converter Pro

基于 Cloudflare Workers 的全能 Serverless 订阅转换与节点中枢。拥有现代深色 UI、SWR 高可用缓存容灾架构、私密配置密码保护锁、智能倍率/专线分组、国旗万国对齐系统，以及 **Argo 隧道 2.0 自动化生成器**。支持将各类代理节点一键转换为 **Sing-Box / Clash Meta (Mihomo) / Surge 5 / Quantumult X / Loon / Base64** 格式，并提供全平台专属唤醒协议（Deep Link）与二维码扫描自动导入。

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/justly110/sub)

---

## 🌟 核心特性

### 1. 🔌 全主流与新兴协议深度解析
- **VLESS**：支持最新 `xhttp` / `splithttp`、`Reality`、`Vision`、`WebSocket (含 ?ed=2560 Early Data 净化)`、`gRPC`。
- **ECH (Encrypted Client Hello)**：自动解析 `&ech=` 参数，在 Sing-Box 与 Clash 中开启 ECH 加密问候，彻底绕过 GFW 的 SNI 阻断。
- **WireGuard / Cloudflare WARP**：双栈 IPv4/IPv6、Reserved 字段与 MTU 完整映射。
- **Shadowsocks-2022**：完整支持 `2022-blake3-*` 多端口与服务端密钥。
- **其他协议**：Trojan、VMess、Hysteria 2 (`hy2`)、TUIC、AnyTLS。

### 2. 📱 全生态客户端适配与一键唤醒 (Deep Link)
- **自适应识别 (Adaptive)**：自动依据请求客户端的 `User-Agent` 返回对应格式。
- **Clash Meta (Mihomo)**：YAML 格式，内置 Fake-IP、DoH 分流、流量嗅探与动态策略组。
- **Sing-Box (1.14+ 现代规范)**：
  - 完整符合 1.14+ 规范，彻底消除 `download_detour`、`missing default_domain_resolver`、`outbound DNS rule` 与 `dns-out` 等废弃警告。
  - 国外代理流量采用 Fake-IP 封装域名，国内/内网流量自动使用 Real-IP 直连。
- **Surge 5**：标准 `.conf` 格式，支持 Proxy、Proxy Group 与分流规则。
- **Quantumult X**：标准 `server_remote` 节点清单格式。
- **Loon**：标准 `[Proxy]` 格式。
- **通用 Base64**：兼容 v2rayNG、PassWall、Shadowrocket 等。
- **🚀 专属唤醒二维码**：
  - 点击 QR Code 图标自动生成客户端专属协议二维码（如 `sing-box://...`、`clash://...`、`surge:///...`）。
  - 手机相机或 App 扫描**全自动填入名称与网址**，亦可点击按钮直接唤醒 App 一键导入。

### 3. 🔐 私密配置密码安全锁 (PAGE_PASSWORD)
- **公私分明**：
  - **公开使用**：通用订阅转换、节点过滤、Argo 隧道生成、客户端订阅更新一律开放。
  - **私密保护**：下方的“已保存的配置”受密码保护，需输入管理密码才能查看、新增或编辑私密节点。
- **记住登录状态**：解锁成功后浏览器（`localStorage`）自动保持登录，重开网页免重复输入，并提供随时“🔒 锁定”按钮。
- **后端安全拦截**：`/favs` 路由全面校验 `X-Password`，未授权请求直接返回 `401 Unauthorized`。

### 4. 🛡️ 99.99% 高可用 SWR 容灾架构 (Zero Downtime)
- **Stale-While-Revalidate + KV 缓存**：远端规则模板自动在边缘缓存，后台异步静默更新。
- **三重容灾降级保证**：`KV 缓存优先` ➔ `GitHub 实时获取` ➔ `内嵌应急模板兜底`，彻底杜绝因 GitHub 429 限流或连接波动导致的转换失败。
- **支持实时穿透**：订阅网址后拼接 `&force=1` 或 `&nocache=1` 即可跳过缓存实时拉取最新规则。

### 5. 🏎️ 智能倍率与专线动态策略组
- **倍率识别**：自动识别节点名称中的倍率特征（如 `0.1x`、`0.5X`、`0.2倍`），并在 Sing-Box 与 Clash Meta 中动态建立“🏎️ 低倍率节点”策略组。
- **专线识别**：自动提取 `IPLC`、`IEPL`、`专线`、`内网` 特征，动态生成“⚡ 专线加速”策略组。

### 6. 🌀 Argo 隧道 2.0 一键生成器
- **优选 IP / 官方域名注入**：支持填入 Cloudflare Clean IP（如 `104.16.80.1`）或优选域名，自动完成连接服务器与 SNI/Host 映射，显著降低延迟。
- **极简 VPS 命令**：脚本自动上传至 KV 缓存，通过 `curl -sSL ... | bash` 极速完成部署。
- **智能探测与修复**：VPS 端自动探测 443 / 80 本地监听端口、TLS 状态与 Host Header 重写。

### 7. 🔍 智能筛选、名称替换与黄金国旗排版
- **双向过滤**：支持“仅保留”与“排除”规则（多组用 `|` 隔开，如 `HK|TW` 或 `5x`），内置 `x`/`X`/`×` 字符兼容匹配。
- **名称替换**：支持 `DEL-关键字`（删除）、`查找-替换`，以及 `ALL-新名称`（一键统改所有节点名称）。
- **黄金 22 地区国旗排序**：自动为节点补上国旗 Emoji，依亚太核心（港、台、日、新、韩）➔ 欧美主流（美、英、加、澳）顺序紧密分群，并自动对重复节点编号。

### 8. 📊 流量与到期日汇总透传
- 自动从上游多个机场获取并汇总上传、下载与总流量，计算最近的到期时间，通过标准 `subscription-userinfo` 标头透传，完美点亮客户端流量信息条。

---

## 🚀 部署教程

### 方法一：一键按钮快速部署 (最推荐、零配置自动托管)

点击本说明文档上方的 **Deploy to Cloudflare Workers** 按钮。

* **零配置自动托管**：Cloudflare 网页部署向导会引导您登录，并**在后台全自动为您创建并对接好所需的 KV 命名空间（`SUB_CACHE`）**。
* **自建 CI/CD (Workers Builds)**：Cloudflare 会在您的 GitHub 下自动创建此项目的复刻仓库。未来只要在 GitHub 修改并 `git push`，Cloudflare 就会自动在端点编译部署。

---

### 方法二：手动 Fork 本项目并使用 GitHub Actions 自动部署 (需配置 Secrets)

如果您选择**手动 Fork 本项目**并利用仓库内置的 GitHub Actions 自动进行 CI/CD 部署，请依照以下步骤操作：

1. **Fork 本项目**：
   点击本仓库右上角的 **`Fork`** 按钮，将项目复制一份到您的 GitHub 账号下。

2. **创建 Cloudflare KV 命名空间**：
   - 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)。
   - 点击左侧菜单的 **`Storage & Databases` (存储和数据库)** ➔ **`KV`**。
   - 点击 **`Create a namespace`**，输入名称（例如 `SUB_CACHE`），创建完成后复制其 **Namespace ID**。

3. **配置 GitHub Repository Secrets**：
   前往您 Fork 出来的 GitHub 仓库页面，依次点击：
   **`Settings`** ➔ **`Secrets and variables`** ➔ **`Actions`** ➔ **`New repository secret`**，添加以下三个密钥：

   | 密钥名称 (Secret Name) | 说明与获取方式 |
   | :--- | :--- |
   | **`CF_API_TOKEN`** | **Cloudflare API 令牌**<br>获取方式：Cloudflare 首页 ➔ 右上角“我的个人资料”➔“API 令牌”➔“创建令牌”➔ 选择“编辑 Cloudflare Workers”模板（需具备 Workers 与 KV 的编辑权限）。 |
   | **`CF_ACCOUNT_ID`** | **Cloudflare 账户 ID**<br>获取方式：登录 Cloudflare ➔ 点击任意域名或 Worker 页面，在右侧栏即可找到“账户 ID (Account ID)”。 |
   | **`CF_KV_ID`** | **KV 命名空间 ID**<br>获取方式：填入步骤 2 中创建的 `SUB_CACHE` 命名空间 ID。 |

4. **触发自动部署**：
   - 前往 GitHub 仓库的 **`Actions`** 标签页。
   - 点击左侧的 **`Deploy to Cloudflare Workers`** 工作流，点击 **`Run workflow`** 手动执行部署。
   - 后续只要您对 `main` 或 `master` 分支推送（Push）任何代码变更，GitHub Actions 就会全自动为您编译并发布至 Cloudflare Workers。

---

### 方法三：本地手动编译部署 (Wrangler CLI)

1. **克隆项目并安装依赖**：
   ```bash
   git clone https://github.com/sammy0101/cf-sub-converter.git
   cd cf-sub-converter
   npm install
   ```

2. **创建 KV 命名空间**：
   ```bash
   wrangler kv:namespace create SUB_CACHE
   ```
   *将终端返回的 `id` 替换至 `wrangler.toml` 中的 `KV_ID_PLACEHOLDER`。*

3. **发布至 Cloudflare**：
   ```bash
   npm run deploy
   ```

---

## 🔐 配置私密管理密码（PAGE_PASSWORD）

若要启用“已保存的配置”安全密码锁，推荐直接在 Cloudflare Dashboard 中设置为 **Secret（加密机密）**，无论重新部署多少次都**永远不会丢失**：

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/) ➔ 点进您的 Worker。
2. 点击顶部的 **`Settings` (设置)** ➔ **`Variables and Secrets` (变量与机密)**。
3. 点击 **`Add variable`** 或 **`Add secret`**：
   - **名称**：`PAGE_PASSWORD`
   - **值**：输入您的管理密码（例如 `MyPass888`）
   - 点击栏位旁的 **`Encrypt` (加密)** 按钮锁定。
4. 点击 **`Save and deploy` (保存并部署)** 即可立即生效！

---

## 📖 使用指南

### 1. 可视化 Web 面板
访问您部署完成的 Workers 网址：
- **数据来源设置**：粘贴机场订阅链接或各类协议节点（支持多行混合输入）。
- **过滤与替换**：设置保留/排除关键字或名称替换规则。
- **短链接云端存储**：设置自定义短代码，规则将自动打包存入 KV。
- **多平台订阅面板**：
  - 复制对应客户端的订阅链接。
  - 点击 QR Code 图标弹出专属唤醒弹窗，手机相机扫描自动填入，或点击“🚀 一键打开并导入”直接唤醒 App。
- **配置收藏管理**：输入管理密码解锁后，可自由新增、编辑、删除或一键套用常用的私密配置。

---

### 2. Argo 隧道 2.0 部署步骤

1. 在网页主输入框粘贴您的 VLESS / VMess 节点内容。
2. 点击 **“第一步：解析并载入当前输入的 VLESS / VMess 节点”**。
3. 勾选欲转换之节点，系统会自动匹配原端口号。
4. （选填）填入 **Cloudflare 优选 IP**（例如 `104.16.80.1`）以加速连接。
5. （选填）填入固定 Tunnel Token 与自定义绑定域名（若留空则为临时随机隧道）。
6. 点击 **“第二步：生成 Argo 一键部署指令与节点”**。
7. 将生成的 `curl -sSL ... | bash` 指令复制至 VPS（以 root 权限执行）。
8. 部署成功后：
   - **固定域名模式**：下方文本框直接复制已转换好的 `_Argo_优选` 节点。
   - **临时随机模式**：VPS 终端将动态输出最终分配的节点链接。

---

### 3. API 调用与外部前端对接

#### 当作标准 SubConverter 后端使用
本项目内置标准 `/sub` 与 `/version` 端点，可直接填入任何开源 `sub-web` 前端的“后端地址 (Backend URL)”：
```text
https://your-worker.workers.dev
```

#### URL 参数手动转换

| 参数 | 说明 | 示例 |
| :--- | :--- | :--- |
| `url` | 原始订阅链接或节点内容（需 URL 编码） | `https://example.com/sub` |
| `target` | 目标格式：`clash` / `singbox` / `surge` / `quanx` / `loon` / `base64` | `target=clash` |
| `include` | 仅保留符合正则之节点 | `include=HK\|TW` |
| `exclude` | 排除符合正则之节点（自动兼容乘号 `×`） | `exclude=5x\|官网` |
| `rename` | 名称替换（删除：`DEL-字符串`、替换：`A-B`、统改：`ALL-名称`） | `rename=DEL-[69云]\|ALL-JP` |
| `force` / `nocache` | 强制穿透 KV 缓存，实时拉取最新远端规则模板 | `force=1` |

**完整调用示例**：
```http
# 转换原始订阅为 Clash Meta 格式，仅保留香港，并删除广告名称
https://your-worker.workers.dev/sub?url=<URL编码>&target=clash&include=HK&rename=DEL-[广告]

# 读取已存于云端 KV 的短链接配置
https://your-worker.workers.dev/<自定义短链接名称>?target=singbox

# 强制刷新缓存获取最新 Sing-Box 规则
https://your-worker.workers.dev/<自定义短链接名称>?target=singbox&force=1
```

---

## 🛡️ 内置分流策略组 (Sing-Box / Clash Meta)

| 图标 | 策略组名称 | 路由逻辑 |
| :--- | :--- | :--- |
| 🏎️ | 低倍率节点 | 自动汇总倍率 `< 1.0x` 的节点（省流专用） |
| ⚡ | 专线加速 | 自动汇总包含 `IPLC` / `IEPL` / `专线` 的低延迟节点 |
| 🚀 | 节点选择 | 手动指定出站节点 |
| ⚡ | 自动选择 | URL Test 自动测速切换最低延迟节点 |
| 💬 | 香港AI 服务 | 针对 OpenAI / Claude / AI Studio 专属分流 |
| 🍎 | 苹果服务 | Apple 相关服务直连或代理 |
| Ⓜ️ | 微软服务 | Microsoft 服务直连或代理 |
| 🎮 | 游戏平台 | Steam / Epic / EA / Ubisoft / Blizzard |
| 🌐 | 非中国 | 全球主流网站（Google、Telegram、YouTube 等） |
| 🇨🇳 | 国内服务 | 中国大陆 IP 与域名自动精准直连 |
| 🏠 | 私有网络 | 局域网 (LAN) 直连 |
| 🛑 | 广告拦截 | 拦截常见广告与追踪器 (AdBlock) |
| 🐟 | 漏网之鱼 | Final Match 未命中规则之默认路由 |

---

## 📁 项目架构

```text
cf-sub-converter/
├── src/
│   ├── index.ts          # Worker 核心路由、并发请求控制、安全鉴权与 API 接口
│   ├── constants.ts      # 响应式深色 UI 模板、QR Code 生成器与 SWR 内嵌降级规则
│   ├── parser.ts         # 万能节点解析器 (VLESS SplitHTTP/EarlyData, ECH, WireGuard, Hy2 等)
│   ├── generator.ts      # 多平台格式生成器 (Sing-Box 1.14+, Clash, Surge 5, QuanX, Loon, Base64)
│   ├── utils.ts          # 倍率与专线特征提取、Base64 安全编码、万国国旗对齐算法
│   └── types.ts          # 严格 TypeScript 类型定义
├── argo.sh               # VPS Argo 隧道 2.0 一键安装与自我修复通用脚本
├── Sing-Box_Rules.JSON   # 远端 Sing-Box 混合 TUN 规则模板 (1.14+ 现代无警告规范)
├── Clash_Rules.YAML      # 远端 Clash Meta (Mihomo) 规则模板
├── wrangler.toml         # Cloudflare Workers 配置文件
└── .github/workflows/
    └── deploy.yml        # GitHub Actions 自动化部署工作流
```

---

## ⚠️ 免责声明

本项目仅供网络安全、分布式架构学习与技术交流使用，不提供任何代理服务器或节点服务。请使用者自觉遵守当地法律法规，切勿用于任何非法用途。