# Cloudflare Tunnel 部署指南

按照以下步骤，通过 Cloudflare Tunnel 把这个个人简介网页部署到你的本地机器/服务器，并通过 Cloudflare 公开访问。

## 前置要求

- 一个 Cloudflare 账号（免费即可）
- 一个域名已经托管在 Cloudflare
- 本地/服务器已经安装了 `cloudflared` 命令行工具

---

## 步骤 1: 安装 cloudflared

### macOS (Homebrew)
```bash
brew install cloudflared
```

### Ubuntu/Debian
```bash
wget -q https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
dpkg -i cloudflared-linux-amd64.deb
```

### 验证安装
```bash
cloudflared --version
```

---

## 步骤 2: 认证 cloudflared

```bash
cloudflared tunnel login
```

这会打开浏览器，让你登录 Cloudflare 并授权 cloudflared 访问你的账号。

---

## 步骤 3: 创建 Tunnel

```bash
# 创建一个名为 profile 的 tunnel
cloudflared tunnel create profile
```

这个命令会生成一个 Tunnel ID 和凭据文件。记下输出的 Tunnel ID。

---

## 步骤 4: 配置路由

在 Cloudflare 控制面板中，为你的子域名添加一条 CNAME 记录，指向你的 Tunnel ID + `cfargotunnel.com`：

```
profile.yourdomain.com -> YOUR-TUNNEL-ID.cfargotunnel.com
```

---

## 步骤 5: 创建配置文件

在当前 `profile` 目录创建 `config.yaml`：

```yaml
url: http://127.0.0.1:8000
tunnel: YOUR-TUNNEL-ID
credentials-file: /Users/YOUR-USERNAME/.cloudflared/YOUR-TUNNEL-ID.json
```

把上面的 `YOUR-TUNNEL-ID` 替换成步骤 3 得到的实际 ID，修改文件路径为你的实际路径。

---

## 步骤 6: 启动本地静态文件服务器

在 `profile` 目录启动一个简单的 HTTP 服务器：

```bash
# 使用 Python 3
cd /Users/jovi/Desktop/profile
python3 -m http.server 8000
```

或者使用 Node.js：

```bash
npx serve . -p 8000
```

---

## 步骤 7: 启动 Cloudflare Tunnel

在另一个终端窗口中：

```bash
# 使用配置文件启动
cloudflared tunnel --config /Users/jovi/Desktop/profile/config.yaml run profile
```

或者直接一条命令：

```bash
cloudflared tunnel --url http://localhost:8000 --name profile
```

---

## 步骤 8: 访问网站

现在你就可以通过 `https://profile.yourdomain.com` 访问你的个人简介网页了！

---

## 后台运行 (作为服务)

如果你想让 Tunnel 在后台一直运行，可以安装为系统服务：

```bash
# macOS
sudo cloudflared service install /Users/jovi/Desktop/profile/config.yaml

# Linux
cloudflared service install /Users/jovi/Desktop/profile/config.yaml
```

然后启动服务：

```bash
# systemd
sudo systemctl start cloudflared
sudo systemctl enable cloudflared
```

---

## 直接通过 Cloudflare Pages 部署（更简单）

如果你只是想托管静态网页，其实 Cloudflare Pages 更简单：

1. 把这个 `profile` 文件夹推送到 GitHub/GitLab
2. 在 Cloudflare Pages 中连接这个仓库
3. 构建命令留空，输出目录设置为 `/`
4. 部署完成就可以直接访问了！

不需要运行 cloudflared，完全免费托管。
