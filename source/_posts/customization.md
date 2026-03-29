---
title: 个性化配置
date: 2026-03-28 23:58
excerpt: 配置您站点的个性化设置。
categories: 快速开始
cover: /hexo-theme-linen-doc-zh-CN/img/vinicius-amnx-amano-17NCG_wOkMY-unsplash.jpg
coverInfo: 
  author: Markus Winkler
  url: https://unsplash.com/photos/a-close-up-of-a-street-sign-on-the-ground-newg0EE_rxw
series: 用户指南
appendRawMarkdown: true
tocType: flat
---

## 配置顶部 Logo

在站点根目录编辑（如果没有，则需要新建一个）`_config.linen.yml` 文件，然后在文件中加入如下格式的内容：

```yaml _config.linen.yml
logo:
  src: '/hexo-theme-linen-doc-zh-CN/img/linen-logo.svg'
  width: 225
  height: 42
```

请将 src、width、height 替换为对应 logo 图片文件的路径和尺寸。

## 配置顶部导航菜单

在 `_config.linen.yml` 中加入如下格式的内容：

```yaml _config.linen.yml
navItems:
  - name: 归档
    path: /archives/
```

## 站点信息

在 `_config.linen.yml` 中加入如下格式的内容：

```yaml _config.linen.yml
info:
  site_desc: Live Young n Act Now.
  avatar: https://xxx.xxx/xx.jpg
  siteCardBg: https://xxx.xxx/xx.jpg
  registration: 火星ICP备22222222
```

