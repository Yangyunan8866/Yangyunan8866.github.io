---
layout: post
title: 用 Jekyll 和 GitHub Actions 发布博客
date: 2026-10-09
excerpt: 一次完整的发布链路：Markdown 写文章，GitHub Actions 构建，GitHub Pages 托管。
tags:
  - 教程
---

这篇文章记录这个博客是怎么发布出去的。整条链路只有三步，而且全都跑在 GitHub 上，本地不需要安装 Ruby、Jekyll、Node.js 或 npm。

## 发布链路

```text
Markdown 文章（_posts/*.md）
        ↓
GitHub Actions 运行 Jekyll 构建
        ↓
生成静态 HTML（_site）
        ↓
发布到 GitHub Pages 网址
```

## 目录结构

| 路径 | 作用 |
| --- | --- |
| `_config.yml` | 站点标题、描述、语言、时区等全局配置 |
| `index.html` | 首页，包含文章列表和项目卡片 |
| `about.md` | 关于页 |
| `_layouts/` | 页面模板，决定所有页面的骨架 |
| `_posts/` | 文章，文件名必须是 `YYYY-MM-DD-标题.md` |
| `assets/style.css` | 全部样式，配色集中在文件顶部的变量里 |

## 工作流做了什么

仓库里的 `.github/workflows/pages.yml` 定义了发布流程：每次推送到 `main` 分支时触发，依次做四件事——

1. 拉取仓库代码
2. 用 Jekyll 把 Markdown 编译成 HTML，输出到 `_site`
3. 把 `_site` 打包成 Pages 制品
4. 部署到 GitHub Pages

所以「发布」这个动作，其实就是一次 `git push`。

## 新增一篇文章的步骤

在 `_posts/` 里新建一个文件，文件名用 `YYYY-MM-DD-英文短标题.md`，开头写好 Front Matter：

```yaml
---
layout: post
title: 文章标题
date: 2026-10-09
excerpt: 一句话摘要，会显示在首页卡片上
tags:
  - 教程
---
```

第二个 `---` 之后就是正文，用普通 Markdown 写就行。提交推送后，Action 会自动重新构建整个站点。

## 几个容易踩的坑

- 文件名里的日期和 Front Matter 里的 `date` 最好一致。如果 `date` 写成了未来的时间，文章默认不会出现在首页。
- 文件名里尽量只用英文字母、数字和连字符，避免空格和特殊符号。
- 改了 `_config.yml` 之后一定要等 Action 跑完再看效果，本地直接双击 `index.html` 是看不到最终页面的，因为它需要经过 Jekyll 处理。

## 小结

这套方案最舒服的地方是「没有构建工具」——不需要 `npm install`，不需要本地起服务，写文章就是编辑文本文件、保存、推送。剩下的交给 GitHub。
