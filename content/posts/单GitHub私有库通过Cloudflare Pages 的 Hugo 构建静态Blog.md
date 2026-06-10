+++
date = '2025-05-08T16:17:11+08:00'
draft = false
title = '单 GitHub 私有库通过 Cloudflare Pages 的 Hugo 构建静态 Blog'

tags  = [ "Hugo", "Cloudflare", "Cloudflare Pages", "Github", "Blog"]

categories = ["IT技术"]

+++

# 单GitHub私有库通过Cloudflare Pages 的 Hugo 构建静态Blog

[TOC]

#Hugo , #Cloudflare , #Cloudflare Pages , #Github , #Blog

希望仅使用一个 GitHub 仓库，通过 Hugo 构建静态博客，并利用 Cloudflare Pages 的 Hugo 自动构建功能进行部署和展示，这完全是可行的，并且也是一种非常高效和简洁的方案。

## **核心思路**

1. **单一仓库策略：** 所有的 Hugo 网站源文件（包括主题）都放在同一个 GitHub 仓库中。
2. **Cloudflare Pages 自动构建：** 配置 Cloudflare Pages 连接你的 GitHub 仓库，并设置构建环境为 Hugo。Cloudflare Pages 会自动检测到你的 Hugo 项目并进行构建和部署。

## **详细步骤和操作代码**

### **第一步：创建 Hugo 网站**

1. **本地环境准备：** 确保你的本地计算机已经安装了 Hugo。你可以访问 https://gohugo.io/installation/ 获取安装指南。

2. **创建 Hugo 站点：** 在你的本地计算机上，打开终端或命令提示符，导航到你希望创建项目的目录，然后运行以下命令：

   Bash

   ```
   hugo new site my-blog
   cd my-blog
   ```

   这将创建一个名为 `my-blog` 的 Hugo 站点目录，并切换到该目录。

3. **添加 Hugo 主题：** 选择一个你喜欢 Hugo 主题。你可以访问 https://themes.gohugo.io/ 浏览并选择。这里我们以一个流行的主题 `PaperMod` 为例。

   Bash

   ```
   git init  # 在你的 Hugo 站点目录下初始化 Git 仓库
   git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
   ```

   这条命令会将 `PaperMod` 主题添加为你的 Hugo 站点的 Git 子模块。

4. **配置 Hugo：** 编辑你的站点配置文件 `config.toml` (或 `config.yaml` 或 `config.json`)，启用主题并进行基本配置。

   Ini, TOML

   ```
   baseURL = "https://blog.kylinwolf.com"  # 将这里替换为你的实际域名（或者 Cloudflare Pages 的默认域名）
   languageCode = "zh-cn"
   title = "WOLF 的 Blog"
   theme = "PaperMod"
   
   [params]
       ShowToc = true
       TocOpen = true
       ShowBreadCrumbs = true
       ShowCodeCopyButtons = true
   
   [menu]
       [[menu.main]]
           identifier = "home"
           name = "首页"
           url = "/"
           weight = 10
   ```

   你可以根据你的需求修改配置文件中的参数。

5. **创建第一篇文章：**

   Bash

   ```
   hugo new posts/my-first-post.md
   ```

   这将在 `content/posts` 目录下创建一个名为 `my-first-post.md` 的 Markdown 文件。编辑该文件，添加你的第一篇文章内容。确保在 Markdown 文件的头部 (Front Matter) 中包含必要的元数据，例如 `title`、`date` 等。

   Markdown

   ```
   ---
   title: "我的第一篇文章"
   date: 2025-05-08T10:00:00+08:00
   draft: false
   ---
   
   这是我的第一篇 Hugo 博客文章。
   ```

6. **本地预览：** 在本地构建并预览你的博客，确保一切正常。

   Bash

   ```
   hugo server -D
   ```

   然后，在你的浏览器中访问 `http://localhost:1313` 查看效果。`-D` 参数会同时构建包括标记为草稿 (draft: true) 的文章。

### **第二步：将 Hugo 站点推送到 GitHub 仓库**

1. **创建 GitHub 仓库：** 在你的 GitHub 账户上创建一个新的公开或私有仓库，仓库名称可以是你喜欢的，例如 `my-hugo-blog`.

2. **添加远程仓库：** 在你的本地 Hugo 站点目录下，将你的本地 Git 仓库与刚创建的 GitHub 仓库关联起来。

   Bash

   ```
   git remote add origin git@github.com:dangerwolf/my-hugo-blog.git
   git branch -M main  # 将本地主分支重命名为 main (如果你的仓库默认分支是 main)
   git add .
   git commit -m "Initial commit of Hugo site"
   git push -u origin main
   ```

   将 `YOUR_GITHUB_USERNAME` 替换为你的 GitHub 用户名，`my-hugo-blog` 替换为你的仓库名称。

### **第三步：配置 Cloudflare Pages**

1. **登录 Cloudflare 账户：** 访问 https://dash.cloudflare.com/ 并登录你的 Cloudflare 账户。
2. **导航到 Pages：** 在左侧导航栏中，找到并点击 "Pages"。
3. **创建新项目：** 点击 "创建项目" (Create a project) 按钮。
4. **连接到 GitHub：** 点击 "连接到 Git 提供商" (Connect to Git) 按钮，并选择 "GitHub"。你需要授权 Cloudflare Pages 访问你的 GitHub 仓库。
5. **选择你的仓库：** 在授权成功后，找到并选择你刚刚创建的 `my-hugo-blog` 仓库。
6. **配置构建设置：** 在 "配置构建设置" (Set up your build settings) 页面，按照以下步骤进行配置：
   - **框架预设 (Framework preset):** 从下拉菜单中选择 "Hugo"。
   - **构建命令 (Build command):** 默认情况下，Cloudflare Pages 会自动识别 Hugo，通常不需要修改。如果需要自定义，可以设置为 `hugo --gc --minify`.
   - **构建输出目录 (Build output directory):** 默认情况下，Hugo 的输出目录是 `public`。确保这里设置为 `public`。
   - **环境变量 (Environment variables):** 你可以根据需要添加环境变量。对于基本的 Hugo 站点，通常不需要设置。如果需要自定义，可以设置为 `HUGO_VERSION` = `0.147.2`。
   - **Web Analytics:** 你可以选择启用 Cloudflare Web Analytics。
7. **完成项目创建：** 点击 "保存并部署" (Save and Deploy) 按钮。

### **第四步：等待 Cloudflare Pages 自动构建和部署**

Cloudflare Pages 会自动拉取你的 GitHub 仓库中的代码，根据你在第三步中配置的 Hugo 构建设置进行构建，并将生成的静态文件部署到 `your-project-name.pages.dev` (这是一个 Cloudflare 提供的默认域名)。

你可以在 Cloudflare Pages 的项目仪表盘中查看构建和部署的进度。一旦部署完成，你的博客就可以通过 Cloudflare 提供的域名访问了。

### **第五步：配置自定义域名 (可选)**

如果你拥有自己的域名，可以在 Cloudflare 中将其添加到你的站点，并将其关联到你的 Cloudflare Pages 项目。具体步骤如下：

1. **添加站点到 Cloudflare：** 如果你的域名还没有在 Cloudflare 中管理，你需要先将其添加到你的 Cloudflare 账户。
2. **在 Pages 中配置自定义域名：** 在你的 Cloudflare Pages 项目仪表盘中，找到 "自定义域" (Custom domains) 选项，然后添加你的域名，并按照 Cloudflare 提供的指引配置 DNS 记录。
