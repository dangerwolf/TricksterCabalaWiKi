# TricksterCabalaWiKi


个人自用卡巴拉岛/星钻物语/Trickster游戏资料wiki。


[TOC]



## 📋 项目概述

- **框架**：Hugo（静态网站生成器）
- **内容语言**：HTML/Markdown
- **主要用途**：个人自用卡巴拉岛/星钻物语/Trickster游戏资料wiki。
- **部署方式**：Git + CI/CD（可选）

## 🚀 快速开始

### 前置要求

- **Hugo**（需要 Extended 版本以支持 SCSS）
  ```bash
  # macOS
  brew install hugo
  
  # Ubuntu/Debian
  sudo apt-get install hugo
  
  # Windows
  choco install hugo-extended
  
  # 验证安装
  hugo version
  ```

### 本地开发环境搭建

1. **克隆仓库**
   ```bash
   git clone https://github.com/dangerwolf/TricksterCabalaWiKi.git
   cd TricksterCabalaWiKi
   ```

2. **初始化或检查依赖**
   ```bash
   # 如果使用了 Hugo Modules，需要初始化
   hugo mod get -u
   
   # 或直接启动开发服务器
   hugo server
   ```

3. **本地预览**
   ```bash
   # 启动实时服务器（默认 http://localhost:1313）
   hugo server
   
   # 详细选项
   hugo server --buildDrafts --buildExpired --buildFuture
   # --buildDrafts: 包含草稿文章
   # --buildExpired: 包含过期文章
   # --buildFuture: 包含未来日期的文章
   ```

## 📝 基本操作

### 1️⃣ 添加新文章

**方法一：使用 Hugo 命令自动生成**
```bash
hugo new posts/my-paper-appendix.md
```

执行后会在 `content/posts/` 目录下创建新文件，包含前置元数据（Front Matter）。

**方法二：手动创建文件**
```bash
# 创建文件
mkdir -p content/posts
touch content/posts/my-paper-appendix.md
```

**文章模板示例**
```markdown
---
title: "论文题目：关于XX的研究"
date: 2024-01-15T10:30:00+08:00
lastmod: 2024-01-15T10:30:00+08:00
draft: false
description: "这篇论文的简要描述"
tags: ["软件工程", "学术研究"]
categories: ["附录"]
author: "Your Name"
---

## 摘要

在此处添加摘要内容。

## 正文

在此处添加论文附录或补充内容。

### 子标题

更详细的内容。
```

**前置元数据字段说明**
| 字段 | 说明 | 示例 |
|------|------|------|
| `title` | 文章标题 | "研究论文标题" |
| `date` | 创建日期 | "2024-01-15T10:30:00+08:00" |
| `lastmod` | 最后修改日期 | "2024-01-15T10:30:00+08:00" |
| `draft` | 是否为草稿 | `true` 或 `false` |
| `description` | 文章摘要（用于SEO）| "简要描述" |
| `tags` | 标签 | `["标签1", "标签2"]` |
| `categories` | 分类 | `["分类1", "分类2"]` |
| `author` | 作者 | "Your Name" |

### 2️⃣ 编写和编辑文章

使用任何文本编辑器编辑 `content/posts/` 下的 `.md` 文件：

```bash
# 推荐编辑器
code content/posts/my-paper-appendix.md    # VS Code
nvim content/posts/my-paper-appendix.md    # Neovim
nano content/posts/my-paper-appendix.md    # Nano
```

**实时预览**：在编辑文件时，保持 `hugo server` 运行，文件保存后浏览器会自动刷新。

### 3️⃣ 编译/生成静态网站

```bash
# 生成静态网站（输出到 public/ 目录）
hugo

# 或带详细输出
hugo --verbose

# 清除并重新生成
rm -rf public/
hugo

# 生成包含草稿的版本
hugo --buildDrafts
```

**输出文件**
```
public/
├── index.html           # 主页
├── posts/              # 文章页面
├── categories/         # 分类页面
├── tags/              # 标签页面
├── css/               # 样式文件
├── js/                # 脚本文件
└── sitemap.xml        # 网站地图（用于SEO）
```

### 4️⃣ 管理草稿和发布

**发布草稿文章**
```bash
# 1. 编辑文章的前置元数据
# 将 draft: true 改为 draft: false

# 2. 更新日期字段
date: 2024-01-20T10:30:00+08:00

# 3. 本地验证
hugo server --buildDrafts

# 4. 编译生成
hugo

# 5. 提交到 Git
git add .
git commit -m "发布新文章：论文名称"
git push origin main
```

### 5️⃣ 常见操作快速查询

| 任务 | 命令 |
|------|------|
| 启动本地服务器 | `hugo server` |
| 添加新文章 | `hugo new posts/filename.md` |
| 编译静态网站 | `hugo` |
| 查看 Hugo 版本 | `hugo version` |
| 清除输出目录 | `rm -rf public/` |
| 验证网站配置 | `hugo config` |

## 🎨 主题配置

### 当前主题

配置文件：`config.toml`（或 `config.yaml`）

```toml
# 基本配置
baseURL = "https://yourdomain.com/"
languageCode = "zh-Hans"
title = "My Hugo Blog"
theme = "your-theme-name"

[params]
  author = "Your Name"
  description = "学术研究和论文附录平台"
```

### 添加新主题

```bash
# 方法一：克隆主题
git clone https://github.com/theme-author/theme-name themes/theme-name

# 方法二：使用 Hugo Modules
hugo mod init github.com/dangerwolf/TricksterCabalaWiKi
hugo mod get -u
```

编辑 `config.toml`：
```toml
theme = "theme-name"
```

## 📂 目录结构

```
TricksterCabalaWiKi/
├── archetypes/         # 文章模板
│   └── default.md     # 默认模板
├── content/           # 文章内容
│   ├── posts/        # 文章目录
│   ├── pages/        # 独立页面
│   └── _index.md     # 主页配置
├── layouts/          # 自定义布局（可选）
├── public/           # 编译输出目录（不提交到 Git）
├── resources/        # 资源文件（缓存等）
├── static/           # 静态资源（图片、文档等）
├── themes/           # 主题目录
├── config.toml       # 站点配置文件
└── README.md         # 本文件
```

## 🔧 高级操作

### 添加代码块高亮

在 Markdown 中使用代码块：

````markdown
```python
def hello_world():
    print("Hello, World!")
```

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```
````

### 插入数学公式

需要在 `config.toml` 中启用 KaTeX 或 MathJax：

```markdown
行内公式：$E=mc^2$

显示公式：
$$
\int_0^\infty e^{-x^2} dx = \frac{\sqrt{\pi}}{2}
$$
```

### 添加图片

```markdown
![图片描述](../images/image-name.png)

或使用 HTML：
<img src="/images/image-name.png" alt="图片描述" width="800"/>
```

将图片放在 `static/images/` 目录下。

### 内部链接

```markdown
[链接文本]({{< relref "/posts/another-post.md" >}})
```

## 📤 部署

### 方式一：GitHub Pages（推荐）

1. **启用 GitHub Pages**
   - 仓库 Settings → Pages
   - Source 选择 "GitHub Actions"

2. **创建 GitHub Actions 工作流**
   
   创建文件 `.github/workflows/hugo.yml`：
   ```yaml
   name: Hugo Deploy
   
   on:
     push:
       branches:
         - main
   
   jobs:
     deploy:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v3
         
         - name: Setup Hugo
           uses: peaceiris/actions-hugo@v2
           with:
             hugo-version: 'latest'
             extended: true
         
         - name: Build
           run: hugo --minify
         
         - name: Deploy
           uses: peaceiris/actions-gh-pages@v3
           with:
             github_token: ${{ secrets.GITHUB_TOKEN }}
             publish_dir: ./public
   ```

3. **提交并推送**
   ```bash
   git add .github/workflows/hugo.yml
   git commit -m "添加 GitHub Actions 部署流程"
   git push origin main
   ```

### 方式二：自助服务器

```bash
# 在本地编译
hugo

# 上传 public/ 目录到服务器
scp -r public/* user@your-server:/var/www/html/

# 或使用 rsync
rsync -avz public/ user@your-server:/var/www/html/
```

### 方式三：Netlify

1. 连接 GitHub 账户到 Netlify
2. 选择仓库
3. 构建命令：`hugo`
4. 发布目录：`public`
5. 自动部署

## 🔍 故障排查

| 问题 | 解决方案 |
|------|--------|
| `command not found: hugo` | 重新安装 Hugo 或检查 PATH |
| 文章不显示 | 检查 `draft: false`，运行 `hugo server --buildDrafts` |
| 样式不加载 | 清除缓存：`rm -rf resources/`，重启服务器 |
| 模块加载失败 | 运行 `hugo mod clean` 和 `hugo mod get -u` |
| 编译缓慢 | 检查 `resources/` 目录大小，考虑启用增量构建 |

## 📚 学习资源

- [Hugo 官方文档](https://gohugo.io/documentation/)
- [Hugo 中文文档](https://www.hugo.blog/)
- [Markdown 语法](https://www.markdownguide.org/)
- [Git 基础教程](https://git-scm.com/book/zh/v2)

## 📝 常用 Git 工作流

```bash
# 1. 创建新分支（可选）
git checkout -b add-new-paper

# 2. 添加和编辑文件
hugo new posts/my-paper.md
# 编辑 content/posts/my-paper.md

# 3. 本地测试
hugo server

# 4. 编译
hugo

# 5. 提交更改
git add .
git commit -m "添加论文：关于XX的研究"

# 6. 推送到远程
git push origin add-new-paper

# 7. 在 GitHub 上创建 Pull Request（可选）
# 或直接推送到 main
git push origin main
```

## 🤝 贡献指南

如需添加或改进内容，请：

1. Fork 本仓库
2. 创建新分支：`git checkout -b feature/your-feature`
3. 提交更改：`git commit -m "添加功能描述"`
4. 推送到分支：`git push origin feature/your-feature`
5. 创建 Pull Request



## 👤 作者

**dangerwolf**

- GitHub: [@dangerwolf](https://github.com/dangerwolf)

---


# 友情赞助商

1. [![Powered by DartNode](https://dartnode.com/branding/DN-Open-Source-sm.png)](https://dartnode.com "Powered by DartNode - Free VPS for Open Source")

2. 开发者需要免费服务的，推荐使用每个月免费$5额度的云服务。
[https://console.run.claw.cloud/signin?link=XHJEEP7HEVIR](https://console.run.claw.cloud/signin?link=XHJEEP7HEVIR)

3. [Cloudcone VPS](https://app.cloudcone.com/?ref=12850)

4. [![This Website is Powered by DigitalPlat FreeDomain Get a free domain from DigitalPlat.](https://img.shields.io/badge/DigitalPlat-Get%20a%20free%20domain%20from%20DigitalPlat.-2563eb?style=flat-square&logo=databricks&logoColor=ffffff)](https://dash.domain.digitalplat.org/signup?ref=3lT6CU6HGe)

5. [DMIT](https://www.dmit.io/aff.php?aff=23825)

