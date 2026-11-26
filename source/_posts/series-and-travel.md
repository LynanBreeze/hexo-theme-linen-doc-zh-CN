---
title: 系列文章与旅行地图
excerpt: 将多篇文章组织成系列，以及旅行系列专属的交互地图与路线规划卡片。
date: 2026-03-28 23:52
cover: /img/duy-le-duc-GUY2f9csQbc-unsplash.jpg
coverInfo:
  author: Duy Le Duc
  url: https://unsplash.com/photos/GUY2f9csQbc
series: 用户指南
tags: [快速开始, 配置]
appendRawMarkdown: true
tocType: flat
---

## 系列文章基础用法

只需在文章的 Front Matter 中添加 `series` 字段，即可将多篇文章归入同一个系列：

```yaml
---
title: 第一篇教程
series: 用户指南
---
```

配置后主题会自动提供以下能力：

- **自动生成系列聚合页**：访问 `/series/<系列名称>/` 即可查看该系列下的全部文章（支持分页，每页篇数遵循 Hexo `_config.yml` 中的 `per_page`）。
- **文章页系列导航**：桌面端右侧栏展示系列目录（最多显示 50 篇，超出时提供聚合页入口）；文章底部提供系列内“上一篇 / 下一篇”导航以及移动端系列目录弹窗。
- **归档页汇总**：在 `/archives/` 归档页与侧边栏站点统计中自动展示系列列表和数量。

## 系列元信息配置（assets-db/series.json）

在站点根目录创建 `assets-db/series.json`，可以为每个系列补充封面图、简介、编号顺序、年份分隔线和双语路径映射等信息：

```json assets-db/series.json
{
  "用户指南": {
    "description": "从零开始配置与使用 Linen 主题的完整指南。",
    "cover": "/img/series-cover.jpg",
    "coverPlaceholder": "/img/series-cover-blur.jpg",
    "coverInfo": {
      "author": "Duy Le Duc",
      "url": "https://unsplash.com/photos/GUY2f9csQbc"
    },
    "noOrder": "asc",
    "yearDivider": false,
    "showMobileIndex": true,
    "mappingName": "User-Guide"
  }
}
```

支持的字段说明：

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `description` | `string` | 系列简介，展示在系列聚合页头部及社交分享 `og:description` 中。 |
| `cover` | `string` | 系列聚合页的顶部头图（也会作为系列页的 `og:image`；旅行系列不展示头图，改为展示交互地图）。 |
| `coverPlaceholder` | `string` | 系列头图的占位图（URL 或 Base64）。 |
| `coverInfo` | `object` | 系列头图右下角的作者或位置信息（格式与文章 `coverInfo` 一致，支持 `author` / `location` 与 `url`）。 |
| `noOrder` | `string` | 设为 `"asc"` 时，移动端系列目录按正序编号（1, 2, 3...）；不设置则默认按倒序编号。 |
| `yearDivider` | `boolean` | 设为 `true` 时，在系列目录中按年份插入年份分隔标题。 |
| `showMobileIndex` | `boolean` | 设为 `false` 时，移动端系列目录弹窗中隐藏序号（默认显示）。 |
| `mappingName` | `string` | 双语站点切换时对应的目标语言系列路径名（例如中文 `用户指南` 映射到英文 `User-Guide`）。 |

## 旅行系列专属功能

当文章的 `series` 设置为 **`旅行`** 或 **`Travel`** 时，主题会自动启用一套面向游记的专属展示模式，包括**旅行地图聚合页**、**游记章节视觉样式**以及**路线规划自动卡片化**。

> 可直接访问本站示例页 [**旅行系列地图演示**](/hexo-theme-linen-doc-zh-CN/series/旅行/) 查看实际渲染效果。

### 1. 交互式旅行地图

访问 `/series/旅行/`（或 `/series/Travel/`）时，页面会自动加载内置的 Leaflet 地图（中文站点使用高德地图瓦片，英文站点使用 OpenStreetMap 瓦片），将所有带有经纬度坐标的游记标记在地图上，并与下方游记足迹卡片列表双向联动（悬停高亮、点击弹出该地点的文章卡片；同一坐标附近的多篇游记会自动聚合计数）。

主题支持以下两种方式为游记提供坐标（按优先级排序）：

- **方式一：在 Front Matter 中配置 `mapPlace`**

  ```yaml
  ---
  title: 关西秋行
  series: 旅行
  mapPlace:
    coordinate: [35.0116, 135.7681] # [纬度, 经度]
    location: 日本·京都
    url: https://maps.apple.com/?ll=35.0116,135.7681
  ---
  ```

- **方式二：自动解析地图链接中的坐标参数**

  如果不单独写 `mapPlace.coordinate`，主题会自动尝试从 `mapPlace.url` 或 `coverInfo.url` 的查询参数中提取 `coordinate=纬度,经度` 或 `ll=纬度,经度`（例如直接粘贴 Apple Maps 的分享链接即可生效）：

  ```yaml
  ---
  title: 澳门漫步
  series: 旅行
  coverInfo:
    location: 澳门·市政署大楼
    url: https://maps.apple.com/place?coordinate=22.193346,113.539592&name=%E5%B8%82%E6%94%BF%E7%BD%B2
  ---
  ```

> 地点显示名称的优先级为：`mapPlace.location > coverInfo.location > 文章 title`。没有解析到有效坐标的旅行文章不会出现在地图标记中。

### 2. 路线规划卡片

在 `旅行` / `Travel` 系列的文章正文中，只要在二级或三级标题 **`路线`**、**`路线规划`**、**`Route`** 或 **`Route Planning`**（英文不区分大小写）下方紧跟一个扁平的无序或有序列表（至少包含 2 项，且不包含嵌套列表、图片、表格或代码块），主题就会自动将其渲染为结构化的路线网格卡片：

```markdown
## 路线规划

- 大阪 2 日（心斋桥、道顿堀）
- 京都 3天2晚（清水寺、岚山）
- 宇治半日
- 奈良 1 日
```

解析规则与特性：

- **自动识别时长**：支持中文/英文多种写法，例如 `2 日`、`3天2晚`、`半日` / `半天` / `half day`、`一日` / `两天` / `一天半`、`大阪2日`、`大阪（2日）`、`3 days`、`2d`、`2 nights`、`4 小时` / `3h` 等。
- **自动识别备注**：列表项末尾括号内若不是时长，会自动提取为地点下方的备注文字（如 `心斋桥、道顿堀`）。
- **比例色条与总计**：当至少有 2 站解析出时长时，卡片上方会自动展示按停留时长等比分配的彩色进度条；当所有站点均为同一时间单位（天/日 或 晚/夜）时，还会自动汇总显示总站数与总天数（例如 `4 站 · 共 6.5 日`）。
