---
title: 个性化配置
date: 2026-03-28 23:58
excerpt: 配置您站点的个性化设置。
categories: 快速开始
cover: /img/vinicius-amnx-amano-17NCG_wOkMY-unsplash.jpg
coverInfo: 
  author: Vinicius "amnx" Amano
  url: https://unsplash.com/photos/17NCG_wOkMY
series: 用户指南
tags: [快速开始, 配置]
appendRawMarkdown: true
tocType: flat
translations: ['en']
---

## 顶部 Logo

在站点根目录编辑（如果没有，则需要新建一个）`_config.linen.yml` 文件，然后在文件中加入如下格式的内容：

```yaml _config.linen.yml
logo:
  src: /img/linen-logo.svg
  width: 225
  height: 42
```

请将 `src`、`width`、`height` 替换为对应 logo 图片文件的路径和尺寸。

如果只需要展示纯文字 Logo，也可以直接配置 `text`：

```yaml _config.linen.yml
logo:
  text: My Blog
```

## 网站图标与资源版本

可以在 `_config.linen.yml` 中自定义网站 Favicon，以及静态 CSS/JS 资源的缓存版本号（会以 `?v=...` 形式附加到样式和脚本 URL 后）：

```yaml _config.linen.yml
icon: /img/favicon.svg # 默认为 /linen-theme/favicon.svg
version: 1.0.0
```

## 顶部导航菜单

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
  site_desc: 一个简约的 Hexo 主题.
  avatar: https://xxx.xxx/xx.jpg
  github: https://github.com/your-name/your-repo
  about: /about/
  siteCardBg: https://xxx.xxx/xx.jpg
  copyright: 本站内容采用 CC BY-NC-SA 4.0 协议授权。
  registration: 火星ICP备22222222
```

- `avatar`：侧边栏作者头像图片。可以在 https://unsplash.com/s/illustrations/avatar?license=free 上找到一些不错的头像图片。
- `github`：顶部导航栏右侧的 GitHub 图标跳转链接。
- `about`：页脚“关于本站”标题的跳转链接（支持站内路径如 `/about/` 或完整外部 URL；不配置时仅显示纯文本标题，不可点击）。
- `siteCardBg`：分享网站时展示的默认 Open Graph 封面图片（`og:image`）。
- `copyright`：自定义页脚版权弹窗（`©`）中的协议说明文案，不配置时使用主题默认多语言文案。
- `registration`：页脚备案号信息。

## 懒加载配置

图片、视频与 `<iframe>` 的懒加载处理需要在 `_config.linen.yml` 中显式启用（`enable: true`）：

```yaml _config.linen.yml
lazyload:
  enable: true
  loadingImage: ""                                      # 默认为空（纯暖纸色骨架微光），也可填写自定义 loading 图片路径
  errorTipImage: /linen-theme/img/lazyload/error-tip.svg # 自定义的 Error 图片
  intersectionRatio: 0.25                               # 触发加载的图片可见比例
  placeholderRatio: 1.5                                 # 默认占位图宽高比（3/2 = 1.5）
  showTransition: true                                  # 是否启用淡入过渡动画
  showAltText: true                                     # 是否将 Alt 文字展示在图片下方
  preloadCount: 5                                       # 预加载的图片数量
  keepPlaceholder: true                                 # 加载完成后是否保留占位容器
```

以上除 `enable` 外均为默认值，可根据实际需要进行修改。修改 `enable` 开关后建议执行 `hexo clean` 清理缓存再重新构建。更多图片占位、灯箱元信息与 HDR 能力请参考 [HDR 与高级图片配置](/hexo-theme-linen-doc-zh-CN/advanced-images/)。

## PhotoSwipe 图片灯箱

主题内置了 [PhotoSwipe](https://photoswipe.com/) 灯箱，需要在 `_config.linen.yml` 中显式开启：

```yaml _config.linen.yml
photoswipe: true
```

全局开启后，如需在某篇文章中单独关闭，可在文章 Front Matter 中添加 `photoswipe: false`。当文章内没有图片或实况照片时，即使开启也不会加载 PhotoSwipe 资源。

## LaTeX 数学公式

如需全局启用内置的 KaTeX 数学公式渲染，可在 `_config.linen.yml` 中添加：

```yaml _config.linen.yml
latex: true
```

也支持按文章按需开启或自定义 KaTeX 选项，详细用法请查看 [LaTeX 数学公式](/hexo-theme-linen-doc-zh-CN/latex/)。

## 追加脚本与样式（heads / appends）

在 `_config.linen.yml` 中可以通过 `heads` 向 `<head>` 中注入自定义 CSS 或脚本，或通过 `appends` 向 `</body>` 之前追加脚本（例如统计代码）：

```yaml _config.linen.yml
heads:
  - <script src="/path-to/your-js.js"></script>
  - <link rel="stylesheet" href="/path-to/your-css.css">
appends:
  - <script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
```

> 提示：文章元信息栏已内置 `<span id="busuanzi_value_page_pv"></span>` 节点，按上述方式接入不蒜子统计脚本后即可自动展示文章阅读量。

## 中英双语站点配置

如果你维护了中英文两个独立域名（或子路径）的站点，可在 `_config.linen.yml` 中配置 `siteOriginLocaleMap`：

```yaml _config.linen.yml
siteOriginLocaleMap:
  zh-CN: https://test.cn
  en: https://test.com
```

配置后还需配合以下内容，导航栏右上角的语言切换按钮才会正确指向对应页面：

1. **文章页**：在文章的 Front Matter 中声明对应的翻译语言，例如中文站文章添加 `translations: ['en']`，英文站文章添加 `translations: ['zh-CN']`（两站的文章路径需保持一致）。
2. **系列 / 分类 / 标签页**：在站点根目录的 `assets-db/` 文件夹下创建对应的 JSON 映射文件，通过 `mappingName` 指定目标语言站点的路径名：
   - `assets-db/series.json`
   - `assets-db/categories.json`
   - `assets-db/tags.json`

以 `assets-db/categories.json` 为例：

```json assets-db/categories.json
{
  "快速开始": {
    "mappingName": "Getting-Started"
  }
}
```