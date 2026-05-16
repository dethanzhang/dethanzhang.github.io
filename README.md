# B#aug 博客管理说明

这是一个基于 Hugo + Stack 主题的静态博客项目。文章、页面和配置都在这个仓库里，推送到 GitHub 后会通过 GitHub Actions 自动发布到 GitHub Pages。

## 目录怎么用

- `content/post/`：博客文章。每篇文章建议一个文件夹，正文写在 `index.md`，配图放同一个文件夹。
- `content/page/`：独立页面，比如归档、搜索、友链。
- `content/categories/`：分类页配置。
- `config/_default/`：站点配置、菜单、主题参数。
- `static/`：全站静态文件，比如 `favicon.png`。
- `assets/scss/custom.scss`：自定义样式。
- `.github/workflows/deploy.yml`：自动构建并发布到 `gh-pages` 分支。

## 本地预览

需要先安装 Hugo Extended 和 Go。

macOS 推荐：

```bash
brew install hugo go
```

启动本地预览：

```bash
hugo server -D
```

然后打开终端提示的地址，通常是：

```text
http://localhost:1313/
```

当前这台机器还没有安装 `hugo`，所以本地预览前需要先安装。

## 新建文章

推荐使用一篇文章一个目录的方式：

```bash
hugo new content/post/my-post/index.md
```

然后编辑：

```text
content/post/my-post/index.md
```

如果文章有封面图，把图片放进同一个目录，例如：

```text
content/post/my-post/cover.jpg
```

文章开头的 Front Matter 示例：

```yaml
---
title: "文章标题"
description: "一句话摘要"
slug: "my-post"
date: 2026-05-16T00:00:00+08:00
image: "cover.jpg"
categories:
  - 随笔
tags:
  - 博客
draft: false
---
```

常用字段：

- `title`：文章标题。
- `description`：摘要，会影响列表页和搜索展示。
- `slug`：文章 URL。当前文章链接格式是 `/p/:slug/`。
- `date`：发布时间。
- `image`：封面图，留空或删除则不显示封面。
- `categories`：分类。
- `tags`：标签。
- `draft`：草稿。`true` 不会正式发布，`false` 会发布。

## 写文章

正文使用 Markdown：

```markdown
## 二级标题

这是一段文字。

![图片说明](cover.jpg)

[链接文字](https://example.com)
```

同目录图片可以直接用文件名引用，比如 `cover.jpg`。

## 发布流程

确认文章不是草稿后提交并推送：

```bash
git status
git add content config assets static README.md archetypes
git commit -m "Add new post"
git push
```

仓库推送到 `master` 后，`.github/workflows/deploy.yml` 会自动构建 Hugo 站点，并把生成结果发布到 `gh-pages` 分支。

站点地址目前配置为：

```text
https://blog.cv999.fun/
```

如果这个域名变了，修改：

```text
config/_default/config.toml
```

里的：

```toml
baseurl = "https://blog.cv999.fun/"
```

## 常见配置

站点标题：

```text
config/_default/config.toml
```

```toml
title = "B#aug"
```

侧边栏签名、头像、评论、颜色模式：

```text
config/_default/params.toml
```

社交链接和菜单：

```text
config/_default/menu.toml
```

自定义 CSS：

```text
assets/scss/custom.scss
```

## 建议先清理的模板内容

现在 `content/post/` 里还有 Stack 主题自带的示例文章：

- `hello-world`
- `image-gallery`
- `markdown-syntax`
- `math-typesetting`
- `shortcodes`

正式使用前可以删除这些示例，或者把它们改成自己的文章。

## 我可以帮你做什么

你可以直接把需求告诉我，例如：

- “帮我新建一篇文章，标题是……”
- “把这段文字整理成博客文章”
- “帮我换头像 / favicon”
- “帮我改站点标题、简介、菜单”
- “帮我删除示例文章”
- “帮我检查为什么 GitHub Pages 没发布”
- “帮我加评论系统 / 统计 / 友链页面”
