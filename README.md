# 个人简介网页

一个简洁美观的个人简介单页网站，使用现代 HTML 和 CSS 构建。

## 特性

- ✨ 简洁现代的设计风格
- 📱 完全响应式，支持移动端和桌面端
- 🌓 支持系统深色模式
- 🎨 使用渐变色彩和柔和阴影
- 🚀 无外部依赖，纯 HTML + CSS
- 🎯 包含完整的个人信息展示模块

## 文件结构

```
profile/
├── index.html   # 主页面
├── style.css    # 样式文件
└── README.md    # 说明文档
```

## 使用方法

直接在浏览器中打开 `index.html` 即可查看效果。

或者使用本地服务器：

```bash
# 使用 Python
python -m http.server 8000

# 或者使用 Node.js
npx serve .
```

然后访问 `http://localhost:8000`

## 自定义

### 修改个人信息

编辑 `index.html` 文件，修改对应部分的内容：

- 基本信息：修改 `.basic-info` 中的内容
- 关于我：修改 `.about` 中的文字
- 技能：修改 `.skill-tags` 中的标签
- 联系方式：修改 `.contact-list` 中的链接

### 修改主题色

在 `style.css` 的 `:root` 部分修改 `--primary-color` 变量即可。

## 浏览器支持

- Chrome (最新)
- Firefox (最新)
- Safari (最新)
- Edge (最新)
