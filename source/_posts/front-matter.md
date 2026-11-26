---
title: 文章配置
excerpt: 一些自定义的 Front Matter 配置。
date: 2026-03-28 23:53
cover: /img/freestocks-VFs2fZEVkXo-unsplash.jpg
coverInfo: 
  author: freestocks
  url: https://unsplash.com/photos/top-view-of-opened-magazine-near-up-of-coffee-VFs2fZEVkXo
series: 用户指南
tags: [快速开始, 配置]
appendRawMarkdown: true
tocType: flat
customComments:
  - text: 比如这里：
    index: 0
    comment: 看到悬浮文案了吗
translations: ['en']
copyright: true
donates:
  - type: wechat
    qrcode: /img/freestocks-VFs2fZEVkXo-unsplash.jpg
sponsors:
  - name: 我
    amount: QQㄋㄟㄋㄟ好喝到咩噗茶
    date: 2026-04-12 
---

## 副标题

为文章设置副标题，会同时展示在文章标题、文章列表、Banner 位、系列目录、浏览器标题与 RSS 中：

```yaml
subTitle: 进阶配置说明
```

## 封面、缩略图与分享图

文章图片相关的 Front Matter 字段如下：

```yaml
cover: /img/cover.jpg
coverPlaceholder: /img/cover-blur.jpg  # 可选，文章头图的占位图（URL 或 Base64）
thumbnail: /img/thumb.jpg              # 可选，文章列表/Banner/相关文章/旅行卡片使用的缩略图，优先级高于 cover
ogImage: /img/og.jpg                   # 可选，社交分享 og:image 封面图
```

其中社交分享图 `og:image` 的优先级为：`系列封面 > ogImage > cover > _config.linen.yml 中的 info.siteCardBg`。

## 封面信息

在封面右下角，可以添加作者或者是位置信息（2选1）。

格式如下：

- 作者信息
  ```yaml
  coverInfo: 
    author: freestocks
    url: https://unsplash.com/photos/top-view-of-opened-magazine-near-up-of-coffee-VFs2fZEVkXo
  ```
- 位置信息
  ```yaml
  coverInfo:
    location: 澳门·市政署大楼
    url: https://maps.apple.com/place?address=Avenida%20de%20Almeida%20Ribeiro%20No.%20163,%20Macao%20SAR,%20China&coordinate=22.193346,113.539592&name=%E5%B8%82%E6%94%BF%E7%BD%B2&place-id=IC211FBD448B1E6C&map=explore
  ```

## 悬浮文字

有的时候想要写一些说明文字，但是又不想总是在文字后面添加括号（比如这样），可以通过添加下面的配置为文字添加悬浮的说明文案。

比如这里：

```yaml
customComments:
  - text: 比如这里：
    index: 0
    comment: 看到悬浮文案了吗
```

## 隐藏文章与 SEO 控制

添加下面的配置可以将文章从首页、归档页中去除，或禁止搜索引擎收录（不会阻止文章生成，仍可通过 URL 直接访问文章页面）。

```yaml
hide:
  recent: true   # 不出现在首页最新文章列表中
  archive: true  # 不出现在归档页及文章计数统计中
  seo: true      # 输出 <meta name="robots" content="noindex, nofollow">
```

## PhotoSwipe 插件

插件来自 [https://photoswipe.com/](https://photoswipe.com/)。

- 全局开启：在 `_config.linen.yml` 中添加 `photoswipe: true`
- 页面级关闭：在全局开启的前提下，于单篇文章 Front Matter 中添加 `photoswipe: false`

当文章内没有图片或实况照片时，即使开启也不会加载 PhotoSwipe 插件。

## 文章目录

在 Front Matter 中有 3 种目录配置：

- 隐藏：`toc: false`
- 默认展开：`tocType: flat`
- 自动折叠展开：<small>什么都不加</small>

## 图片懒加载

需要在 `_config.linen.yml` 中显式配置开启懒加载处理：

```yaml _config.linen.yml
lazyload:
  enable: true
```

修改开关后需要执行 `hexo clean`（或 `npm run clean`）清除已构建的缓存，否则对已生成文章不会生效。

如果需要针对单篇文章覆盖加载后是否保留占位容器，可以在 Front Matter 中配置：

```yaml
lazyload:
  keepPlaceholder: false
```

如果只想要针对某些图片（或 `<video>`、`<iframe>`）取消懒加载，可以使用以下格式引用图片：

- `![no-lazy](https://abc.com/def.jpg)`

- `![This is a image $no-lazy](https://abc.com/def.jpg)`

- `<img no-lazy src="https://abc.com/def.jpg" alt="def">`

关于 `$no-link`、`$aspect-ratio`、`$placeholder`、`assets-db/imgs/*.json` 以及 HDR 切换等高级图片能力，请参阅 [HDR 与高级图片配置](/hexo-theme-linen-doc-zh-CN/advanced-images/)。

## 查看原始 Markdown 内容

在文章 Front Matter 中添加以下配置后，文章顶部元信息栏会出现“查看原始 Markdown 内容”切换按钮，方便读者查看或复制文章源码：

```yaml
appendRawMarkdown: true
```

## 文章时效性提示

对技术教程或时效性较强的内容，可以在 Front Matter 中开启时效性提示。当文章发布超过 **180 天** 后，正文顶部会自动展示过期提醒横幅：

```yaml
ageWarning: true
```

## 阅读时间与字数统计

默认会在文章顶部同时展示预计阅读时间、字数与图片数。如果只想保留预计阅读时间、隐藏字数和图片数统计，可添加：

```yaml
readTime:
  count: false
```

## 单篇文章关闭评论区

如果站点已全局开启 Gitalk，可以在某篇文章中单独关闭评论区：

```yaml
comment: false
```

## 页面级注入 `<head>` 内容

如需仅在当前文章的 `<head>` 中引入特定样式或脚本，可使用 `heads` 字段：

```yaml
heads:
  - <link rel="stylesheet" href="/css/custom-post.css">
  - <script src="/js/custom-post.js" defer></script>
```

## 语言与双语翻译关联

可以单独指定文章语言（影响日期格式、字数统计方式、Gitalk 语言与 `og:locale`），并声明目标翻译语言以显示顶部语言切换按钮（需配合 `_config.linen.yml` 中的 `siteOriginLocaleMap`）：

```yaml
language: zh-CN
translations: ['en']
```

## 相关文章

当文章含有 >=2 个相同的标签时，则认为它们是相关的，会在页面底部展示跳转入口。

如果想要不展示这篇文章下面的相关文章入口，在文章的 Front Matter 中添加这个配置：

```yaml
showRelated: false
```

## 版权信息

当你想要在文章内容底部加一个版权信息提示，在文章的 Front Matter 中添加这个配置：

```yaml
copyright: true
```

## 赞赏二维码与赞赏列表

在文章的 Front Matter 中配置赞赏二维码：

```yaml
donates:
  - type: wechat
    qrcode: /img/wx_qr.jpg
```

如果希望在赞赏按钮下方同时展示致谢名单，可以继续添加 `sponsors`（注意：`sponsors` 需与 `donates` 同时配置才会渲染）：

```yaml
sponsors:
  - name: 我
    amount: QQㄋㄟㄋㄟ好喝到咩噗茶
    date: 2026-04-12
```

## 更多专题配置

以下高级 Front Matter 字段已单独成文介绍：

- **系列文章与旅行地图**（`series`、`mapPlace`）：见 [系列文章与旅行地图](/hexo-theme-linen-doc-zh-CN/series-and-travel/)
- **LaTeX 数学公式**（`latex` / `math`）：见 [LaTeX 数学公式](/hexo-theme-linen-doc-zh-CN/latex/)
- **HDR 图片切换**（`hdrSwitch`、`hdrAssetsPrefix`）：见 [HDR 与高级图片配置](/hexo-theme-linen-doc-zh-CN/advanced-images/)