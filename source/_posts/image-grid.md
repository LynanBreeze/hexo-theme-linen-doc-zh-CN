---
title: 图片排版
excerpt: 简单的排版更易阅读。
date: 2026-03-28 23:55
cover: /img/ivan-shimko-PhciG8fpRKw-unsplash.jpg
coverInfo: 
  author: Ivan Shimko
  url: https://unsplash.com/photos/three-beach-illustrations-PhciG8fpRKw
series: 用户指南
tags: [快速开始, 配置]
appendRawMarkdown: true
tocType: flat
translations: ['en']
---

Markdown 默认的图片是一行一张。

![](/img/duy-le-duc-GUY2f9csQbc-unsplash.jpg)

Linen 主题新增了图片容器，支持以下几种布局的图片排版。请点击页面上的 **切换到原始 Markdown 内容** 按钮参考页面源码来使用图片排版。

## 横排

:::image-grid landscape
![](/img/klara-kulikova-PgrSvkU1_4Y-unsplash.jpg)
![](/img/mariola-grobelska-rxFb6meV3ck-unsplash.jpg)
:::

## 竖排

:::image-grid portrait
![](/img/kamran-norollahi-KwP58z9zJeE-unsplash.jpg)
![](/img/julian-scholl-Wf6MhLHePSI-unsplash.jpg)
![](/img/david-boca-Xqmj-oQ_Nek-unsplash.jpg)
:::

## 横竖混排

支持以下 6 种混排比例布局：

- **3:2 与 2:3 混排**：`r73`（左横右竖）、`r37`（左竖右横）
- **4:3 与 3:4 混排**：`r64`（左横右竖）、`r46`（左竖右横）
- **16:9 与 9:16 混排**：`rLeftWide`（左宽右竖）、`rRightWide`（左竖右宽）

:::image-grid r73
![](/img/jasper-gribble-EOMFC1NyHgM-unsplash.jpg)
![](/img/squids-z-ShAHqWGOrRU-unsplash.jpg)
:::

## 横向滚动相册（scroll / slider）

当有多张图片希望在同一区域内横向滑动浏览时，可以使用 `scroll` 或 `slider`（两者等价，均支持 `scroll-snap` 吸附对齐）：

:::image-grid scroll
![](/img/klara-kulikova-PgrSvkU1_4Y-unsplash.jpg)
![](/img/mariola-grobelska-rxFb6meV3ck-unsplash.jpg)
![](/img/pine-watt-2Hzmz15wGik-unsplash.jpg)
:::

## 选项卡切换器（switcher）

当需要对多张图片做对比展示（例如不同光线、不同构图或不同方案的效果对比）时，可以使用 `switcher` 布局：

- 可以通过 `标签名 | ![](图片地址)` 显式指定底部切换按钮文案；
- 也可以直接通过图片的 `alt` 文本作为按钮文案（若两者同时存在，优先使用 `alt`）；
- 未提供时默认按序号 `1`、`2`、`3` 显示；
- 点击进入 PhotoSwipe 灯箱并左右切换图片时，页面的当前选中选项卡也会自动同步。

:::image-grid switcher
![方案一](/img/klara-kulikova-PgrSvkU1_4Y-unsplash.jpg)
![方案二](/img/mariola-grobelska-rxFb6meV3ck-unsplash.jpg)
![方案三](/img/pine-watt-2Hzmz15wGik-unsplash.jpg)
:::

> 提示：普通 `:::image-grid` 不带额外类名时也支持 2～4 列自适应排版，且容器内除了图片外同样支持嵌套 `<iframe>`（例如实况照片）。