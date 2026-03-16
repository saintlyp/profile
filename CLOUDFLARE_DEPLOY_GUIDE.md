# 🚀 Cloudflare Pages 部署详细指南

本指南带你一步步将个人简介网页部署到 Cloudflare Pages，完全免费，自带 HTTPS 和 CDN。

## 📋 前置检查 ✅

- [x] 代码已推送到 GitHub: **https://github.com/saintlyp/profile**
- [x] 你已有 Cloudflare 账号
- [x] 你的域名已托管在 Cloudflare（如果要绑定自定义域名的话）

---

## 第一步：登录 Cloudflare 控制台

1. 打开 https://dash.cloudflare.com/
2. 登录你的 Cloudflare 账号

---

## 第二步：进入 Pages 功能

在左侧边栏（蓝色那一列）找到 **Pages**，图标像一个网页，点击它。

> 如果没找到，往下滚动鼠标，在"Compute" 分类下面。

---

## 第三步：创建新项目

1. 进入 Pages 页面后，点击右上角的蓝色按钮 **"Create a project"**
2. 你会看到三个选项：
   - **Connect to Git** ← 👉 **选这个！**
   - Direct upload
   - ...

3. 如果你是第一次连接，Cloudflare 会提示你连接 GitHub 账号：
   - 点击 **"Connect GitHub"**
   - 会跳转到 GitHub，授权 Cloudflare 访问你的仓库
   - 按照提示完成授权，跳转回 Cloudflare

---

## 第四步：选择仓库

1. 授权完成后，Cloudflare 会列出你 GitHub 上所有仓库
2. 在搜索框输入 **profile** 或者找到 **saintlyp/profile**
3. 点击选中它
4. 点击 **"Begin setup"** 按钮进入下一步

---

## 第五步：配置构建设置 ⚙️

这是最关键的一步，按下图填：

| 设置项 | 填写内容 | 说明 |
|--------|----------|------|
| **Production branch** | `main` | 默认就是 main，不用改 |
| **Build command** | **留空！什么都不写！** | 我们是纯静态 HTML/CSS，不需要构建 |
| **Build output directory** | **`/`** （就是一个斜杠）| 告诉 Cloudflare 根目录就是输出目录 |

其他设置保持默认就好。

---

## 第六步：部署！🚀

1. 检查一下设置是否正确：
   - 构建命令是空的 ✅
   - 输出目录是 `/` ✅
   
2. 点击底部的 **"Save and Deploy"** 按钮

3. Cloudflare 开始部署，你会看到部署进度：
   - Cloning repository（克隆代码）
   - Installing dependencies（安装依赖，因为我们不需要，这步很快）
   - Building site（构建，跳过）
   - Deploying...（部署）

4. 整个过程大约 **1-2 分钟**

---

## 第七步：完成部署 ✅

部署成功后，你会看到：
- 绿色的 "Deployed" 状态
- Cloudflare 会给你一个默认域名，格式像这样：
  ```
  profile-saintlyp.pages.dev
  ```
- 你可以直接点击这个域名访问你的网站！🎉

---

## （可选）绑定你的自定义域名 🌍

如果你想用上自己的域名，比如 `profile.yourdomain.com`：

1. 在项目页面，点击 **"Custom domains"** 标签
2. 点击 **"Set up a custom domain"**
3. 输入你的域名（比如 `profile.yourdomain.com`）
4. 点击 **"Continue"**
5. Cloudflare 会自动检查 DNS 设置：
   - 如果你的域名已经在 Cloudflare 上，它会自动添加对应 DNS 记录
   - 不需要你手动操作
6. 点击 **"Activate domain"**
7. 等待 1-2 分钟，证书生效，就可以用你的域名访问了！

---

## 第八步：查看和管理部署

### 查看部署日志
在项目页面 → **"Deployments"** 标签，可以看到所有部署记录。

### 重新部署
当你更新了 GitHub 上的代码，Cloudflare Pages 会**自动重新部署**，不用手动操作。

### 回滚到旧版本
如果新版本出问题了，在 Deployments 页面找到旧版本，点三个小圆点 → **"Retry deployment"** 即可。

---

## 🔄 更新网站内容

以后你改了代码，只要推送到 GitHub main 分支，Cloudflare Pages 会自动检测到并重新部署：

```bash
cd /Users/jovi/Desktop/profile
# 修改你的代码...
git add .
git commit -m "Update website content"
git push origin main
```

然后去 Cloudflare Pages 看一眼，几分钟就部署好了。

---

## ❌ 常见问题解决

### 1. 部署失败了怎么办？

点击进入 **"Deployments"** → 看失败那次的 **"View build log"**，看错误信息。

最常见错误：
- **输出目录不对** → 确认填的是 `/`
- **有 build 命令导致错误** → 确认 Build command 留空

### 2. 打开网页显示空白？

检查 `index.html` 是否在仓库根目录，我们这里是对的，所以不会有这问题。

### 3. 修改后不更新？

在部署页面点三个小圆点 → "Retry deployment" 手动触发。

---

## 🎉 完成后

部署成功后，你会得到：
- 一个永久免费的静态网站
- 自动 HTTPS 证书
- 全球 CDN 加速，访问速度快
- 自动 CI/CD，改代码推 GitHub 就自动更新
- 不需要管服务器，不用维护

---

## 🌐 示例效果

部署完成后网址类似：
- 默认: `https://profile-saintlyp.pages.dev`
- 自定义: `https://profile.yourdomain.com`

打开就能看到你的个人简介网页了！
