---
title: 更新日志（本网站）
author: 夜輪風超絶技巧変奏曲
date: 2022-11-16
category: Change Log
layout: post
---

## 2023.9.15

- 添加中文搜索支持。
- 修改底部导航栏样式。
- 添加了域名迁移的告示。

## 2023.9.1

- 现在该文档也同时托管在 Cloudflare 上。
- 中文与英文文档分割到了不同的 GitHub 仓库中。
- 启用新域名 <zh.ceviodoc.uk>。
- 移除 mkdocs-static-i18n 插件。

## 2022.11.21

- 新增英文翻译。
- 为切换中文与英文页面，语言切换功能已启用。
    - 添加了 mkdocs-static-i18n 插件。
    - 由于语言切换与 `navigation.instant` 不兼容，现已停用该选项。
        - > mkdocs-material language switcher contextual link is not compatible with theme.features = navigation.instant
- 由于文件夹结构发生变化，所有页面的创建日期均发生了改变。
- 添加了图片缩放功能。
    - 添加了 mkdocs-glightbox 插件。

## 2022.11.16

- Material for MkDocs 更新到 8.5.10。
    - Admonition 的样式变化发生于版本 8.5.6 中 。
- 现在，每个页面的最下方将显示它的创建日期。
    - 对 git-revision-date-localized 插件做了如下设置：`enable_creation_date: true`。

## 2022.6.7

初版完成。
