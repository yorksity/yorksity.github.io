# York's Blog

我的个人技术博客，记录编程学习与工程实践中的思考、踩坑与总结。

基于 [Jekyll](https://jekyllrb.com/) 构建，通过 [GitHub Actions](.github/workflows/jekyll-gh-pages.yml) 自动部署到 [GitHub Pages](https://pages.github.com/)。

## 技术栈

- **静态站点生成器**：Jekyll
- **模板引擎**：Liquid
- **Markdown 渲染**：kramdown
- **代码高亮**：Rouge
- **托管**：GitHub Pages

## 目录结构

```
├── _config.yml              # 站点配置
├── _layouts/                # 页面布局（default、post）
├── _includes/               # 可复用组件（head、header、footer）
├── _posts/                  # 博客文章（Markdown）
├── assets/css/              # 样式文件
├── index.html               # 首页（文章列表）
└── .github/workflows/       # CI/CD 自动部署
```

## 本地开发

```bash
# 安装依赖
bundle install

# 启动本地服务器（默认 http://localhost:4000）
bundle exec jekyll serve
```

## 撰写文章

在 `_posts/` 目录下新建文件，命名为 `YYYY-MM-DD-title.md`，文件头使用如下 front matter：

```markdown
---
layout: post
title: "文章标题"
date: 2026-08-24 00:00:00 +0800
tags: [标签1, 标签2]
---
```

## 部署

推送代码到 `main` 分支，GitHub Actions 会自动构建并部署，无需手动操作。

## License

[MIT](LICENSE)