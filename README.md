# 不死的小强2.0 · 个人博客

这是一个 Jekyll 静态个人博客，文章写在 `_posts/*.md`，推送到 `main` 后由 GitHub Actions 自动构建并发布到 GitHub Pages。

- 线上网址：<https://yangyunan8866.github.io/>
- 仓库：<https://github.com/Yangyunan8866/Yangyunan8866.github.io>
- 技术栈：Markdown + Jekyll + GitHub Actions + GitHub Pages
- 不依赖 React、Vue、Node.js、npm、外部 CDN 或本地构建工具

## 目录结构

```text
_config.yml                 站点标题、描述、语言、时区
index.html                  首页：个人介绍、文章列表、项目卡片
about.md                    关于页
_layouts/default.html       全站骨架（导航、页脚、head）
_layouts/post.html          单篇文章模板
_posts/*.md                 文章，文件名格式 YYYY-MM-DD-title.md
assets/style.css            全部样式，配色集中在文件顶部 CSS 变量
.github/workflows/pages.yml 自动构建与发布工作流
```

## 本地预览说明

仓库里的 `index.html` 是 Jekyll 模板源码，**双击本地文件看不到最终页面**，因为它需要经过 Jekyll 处理。最终 HTML 由 GitHub Actions 生成，所以本地不需要安装 Ruby、Jekyll、Node.js 或 npm。

## 写一篇新文章

在 `_posts/` 中新建文件，文件名使用：

```text
YYYY-MM-DD-title.md
```

开头保留 Front Matter：

```yaml
---
layout: post
title: 文章标题
date: 2026-10-09
excerpt: 一句话摘要
tags:
  - 学习
---
```

第二个 `---` 之后直接写 Markdown 正文：标题、段落、列表、链接、代码块都可以使用。

注意：文件名里的日期要和 Front Matter 里的 `date` 一致；如果 `date` 是未来时间，文章默认不会出现在首页。

## 发布流程

1. 修改或新增 `_posts/*.md`。
2. 修改首页内容时编辑 `index.html`。
3. 修改关于页时编辑 `about.md`。
4. 修改配色和排版时编辑 `assets/style.css`。
5. `git diff` 检查变更。
6. `git add`、`git commit`、`git push`。
7. GitHub Actions 自动运行 Jekyll，将 Markdown 编译成 HTML 并发布到 GitHub Pages。

## 配色

所有颜色集中在 `assets/style.css` 顶部的 `:root` 变量里，改这几个值就能整体换色：

| 变量 | 当前值 | 用途 |
| --- | --- | --- |
| `--ink` | `#15263a` | 正文与标题文字 |
| `--muted` | `#5c7086` | 次要文字 |
| `--paper` / `--paper-2` | `#f7fafd` / `#eaf3fa` | 页面与卡片底色 |
| `--pink` | `#2f7fb5` | 主色（分隔线、引用边、强调） |
| `--pink-dark` | `#1f5f8c` | 主色加深（链接、标签、小标题） |
| `--mint` | `#3fa8a0` | 点缀色（关于页左边框） |

## 构建流程图

```text
Markdown 文章
      ↓
Jekyll / GitHub Actions
      ↓
HTML 页面
      ↓
GitHub Pages 网址
```

## Agent 提示词

```text
/goal 这是一个 Jekyll 静态博客项目，文章写在 _posts/*.md。
请先读取 README、_config.yml、index.html、_layouts 和 _posts，再动手修改。
新增文章时只在 _posts/ 中创建 YYYY-MM-DD-title.md，并使用现有 Front Matter 和 layout: post。
不要引入 React、Vue、Node.js、npm、外部 CDN 或新的构建工具；不要重写整个模板。
修改前先列出文件和计划；修改后检查 Markdown Front Matter、文章链接、相对资源路径和 Git diff。
我确认之后才执行 git commit 和 git push。
```
