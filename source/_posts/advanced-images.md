---
title: HDR 与高级图片配置
excerpt: 了解 HDR/SDR 图片切换、内联图片控制指令、视频/实况照片懒加载以及 assets-db/imgs 图片元数据库。
date: 2026-03-28 23:50
cover: /img/mariola-grobelska-rxFb6meV3ck-unsplash.jpg
coverInfo:
  author: Mariola Grobelska
  url: https://unsplash.com/photos/rxFb6meV3ck
series: 用户指南
tags: [快速开始, 配置]
appendRawMarkdown: true
tocType: flat
hdrSwitch: true
hdrAssetsPrefix: hdr-demo/hdr
translations: ['en']
---

## HDR / SDR 图片切换

对于包含 HDR 摄影作品的文章，Linen 支持在 HDR 与 SDR 资源之间无刷新切换。

### 效果演示

本页已配置 `hdrSwitch: true` 与 `hdrAssetsPrefix: hdr-demo/hdr`。在支持 HDR 的屏幕和浏览器上，点击顶部导航栏右侧的 **HDR 开关** 即可实时切换下方示例照片的 HDR / SDR 资源：

![HDR / SDR 切换示例（图片版权归 lynan 所有）](/img/hdr-demo/sdr/DSC08834.jpg)

### 1. 开启方式

在文章的 Front Matter 中配置 `hdrSwitch` 和 `hdrAssetsPrefix`：

```yaml
---
title: 冰岛极光摄影
hdrSwitch: true
hdrAssetsPrefix: photos/hdr # 也可填写完整前缀，如 https://cdn.example.com/photos/hdr
---
```

### 2. 路径命名规范

- `hdrAssetsPrefix` 路径中必须包含 `/hdr`（推荐写相对路径片段如 `hdr-demo/hdr`，可同时兼容根路径与子路径部署）。
- 主题会自动将其中的 `/hdr` 替换为 `/sdr` 作为对应的 SDR 前缀（例如 `hdr-demo/sdr`）。
- 在 Markdown 正文中默认引用 `/sdr/` 路径的图片；当开启 HDR 时，主题会自动把正文图片、`lazyload` 占位数据以及 PhotoSwipe 灯箱链接中的 SDR 前缀替换为 HDR 前缀。

### 3. 自动检测与交互

- 主题通过 `matchMedia('(dynamic-range: high)')` 与 `CSS.supports('dynamic-range-limit: no-limit')` 检测当前屏幕和浏览器是否真正支持 HDR 图像渲染。
- 在满足 HDR 条件且视口宽度 ≥ `500px` 的设备上，打开文章时会自动切换至 HDR 模式；读者也可以随时点击顶部导航栏右侧的 **HDR 开关** 在 HDR/SDR 之间手动切换。
- 配合 PhotoSwipe 灯箱查看图片 EXIF 时，处于 HDR 激活状态的照片还会显示 `HDR` 标识。

## Markdown 图片内联指令

当在 `_config.linen.yml` 中开启 `lazyload.enable: true` 后，除了常规的 `alt` 描述文字，还可以在图片的 `alt` 文本或 HTML 属性中嵌入以下控制指令（渲染到页面下方图注时，指令会自动被清理，不会展示给读者）：

| 指令 | 作用 | 示例 |
| --- | --- | --- |
| `no-lazy` / `$no-lazy` | 禁用该图片的懒加载包装 | `![风景 $no-lazy](/img/a.jpg)` |
| `no-link` / `$no-link` | 禁用点击进入 PhotoSwipe 灯箱放大 | `![示意图 $no-link](/img/b.jpg)` |
| `$aspect-ratio=W/H=aspect-ratio` | 为单张图片指定占位图宽高比，减少页面抖动 | `![宽幅图 $aspect-ratio=16/9=aspect-ratio](/img/c.jpg)` |
| `$placeholder=值=placeholder` | 为单张图片指定自定义占位图（URL 或 `data:image/...`） | `![图注 $placeholder=https://.../blur.jpg=placeholder](/img/d.jpg)` |

如果直接书写 HTML `<img>` 标签，也可以通过原生属性控制：

```html
<img
  src="https://cdn.example.com/photo.jpg"
  alt="照片描述"
  style="aspect-ratio: 3/2;"
  data-placeholderimg="data:image/jpeg;base64,..."
  pswp-src="https://cdn.example.com/photo-original.jpg"
/>
```

- `no-lazy`、`no-link` 同样可直接作为 HTML 属性写在 `<img>` 上。
- `pswp-src` 可用于指定点击灯箱后加载的高清原图地址。

## 视频、iframe 与实况照片（Live Photo）

开启 `lazyload.enable: true` 后，正文中的 `<video>` 与 `<iframe>` 元素也会自动接入懒加载（同样支持 `no-lazy` 属性跳过，并可读取 `style="aspect-ratio: ..."` 计算占位比例）。

此外，若使用包含 `/static/live-photo/` 路径的 `<iframe>` 嵌入实况照片（URL 查询参数中提供 `picUrl` / `photoSrc` 与 `videoUrl` / `videoSrc`，可选 `muted`、`loop`、`volume`），并开启了 `photoswipe: true`，主题会自动将其纳入 PhotoSwipe 灯箱相册，在灯箱大图视图中同样支持点击 **LIVE** 按钮播放动态画面。

## 图片元数据库（assets-db/imgs/*.json）

如果站点图片较多，不希望在每篇 Markdown 中手写宽高、占位图或 EXIF 信息，可以在站点根目录下创建 `assets-db/imgs/` 目录，并放入一个或多个 `.json` 文件（每个文件为一个 JSON 数组，构建时会自动合并读取）。

主题在构建时会自动按 URL（比较 `pathname + search + hash`，忽略域名差异）匹配正文图片和文章封面图 `cover`，并注入对应的占位比例、占位图、多语言图注和灯箱 EXIF。

### JSON 结构示例

```json assets-db/imgs/2026.json
[
  {
    "url": "https://cdn.example.com/photos/sdr/tokyo-tower.webp",
    "width": 1600,
    "height": 1067,
    "originalUrl": "https://cdn.example.com/photos/sdr/tokyo-tower-full.jpg",
    "placeholder": "blurhash:LGF5]+Yk^6#M@-5c,1J5@[or[Q6.",
    "alt": "暮色中的东京塔",
    "alten": "Tokyo Tower at Dusk",
    "caption": "拍摄于六本木展望台",
    "caption_en": "Taken from Roppongi Hills",
    "exif": "{Sony A7C II}{ISO 100}{35mm}{f/2.8}{1/500s}{0 EV}{FE 35mm F1.8}{1}",
    "location": "https://maps.apple.com/?ll=35.6586,139.7454",
    "locationText": "东京塔",
    "locationText_en": "Tokyo Tower",
    "noLink": false
  },
  {
    "url": "https://cdn.example.com/photos/sdr/tokyo-tower-full.jpg",
    "width": 4000,
    "height": 2667
  }
]
```

### 字段说明

| 字段 | 说明 |
| --- | --- |
| `url` | 图片 URL，用于与文章中的图片 `src` 或 `cover` 匹配。 |
| `width` / `height` | 图片像素宽高，用于计算占位图比例和 PhotoSwipe 尺寸。 |
| `originalUrl` | 点击 PhotoSwipe 灯箱时加载的高清原图地址；如果该地址也在元数据库中有对应条目，灯箱会自动使用原图条目的 `width`/`height`。 |
| `placeholder` | 占位图，支持普通图片 URL、Base64 `data:image/...`，以及以 `blurhash:` 开头的 BlurHash 字符串。 |
| `alt` / `alt<语言>` | 图片下方展示的图注文字（优先匹配带站点语言后缀的字段，例如 `altzh-CN`、`alten`，找不到则回退到 `alt`）。 |
| `caption` / `caption_<语言>` | PhotoSwipe 灯箱内展示的说明文字（例如 `caption_zh-CN`、`caption_en`）。 |
| `exif` | 灯箱底部展示的拍摄参数，按固定顺序用花括号包裹 8 项：`{相机}{ISO}{焦距}{光圈}{快门}{曝光补偿}{镜头}{是否HDR}`（某项为空可留空 `{}`）。 |
| `location` | 拍摄地点的地图链接（配合 `exif` 一起在灯箱中展示）。 |
| `locationText` / `locationText_<语言>` | 拍摄地点的展示名称（支持按语言匹配，如 `locationText_zh-CN`、`locationText_en`）。 |
| `noLink` | 设为 `true` 时禁用该图片的灯箱点击放大。 |
