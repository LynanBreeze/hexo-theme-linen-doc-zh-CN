---
title: 网站 RSS
date: 2026-03-28 23:56
cover: /img/markus-winkler-GdpDAj8unB4-unsplash.jpg
coverInfo: 
  author: Markus Winkler
  url: https://unsplash.com/photos/a-wooden-block-spelling-subscribe-on-a-table-GdpDAj8unB4
series: 用户指南
tags: [快速开始, 配置]
appendRawMarkdown: true
tocType: flat
translations: ['en']
---

无需另外安装插件，默认可生成 RSS 文件。

支持的配置项如下：

```yaml _config.linen.yml
feed:
  path: /feed.xml                  # 默认 /feed.xml
  limit: 10                        # 默认 10（输出最新文章篇数）
  icon: /linen-theme/favicon.svg   # 建议显式配置站点图标路径或完整 URL
```

可以按需修改以上 3 个 RSS 配置选项。其中 `icon` 未设置默认值，建议显式填写站点图标的站内路径或完整 `https://` 地址。

如果需要关闭 RSS 插件（或是使用其他的 RSS 插件），可添加下面的配置来关闭内置的 RSS 插件：

```yaml _config.linen.yml
feed: false
```