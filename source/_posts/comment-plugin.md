---
title: 评论区插件
date: 2026-03-28 23:54
cover: /img/volodymyr-hryshchenko-V5vqWC9gyEU-unsplash.jpg
coverInfo: 
  author: Volodymyr Hryshchenko
  url: https://unsplash.com/photos/three-crumpled-yellow-papers-on-green-surface-surrounded-by-yellow-lined-papers-V5vqWC9gyEU
series: 用户指南
appendRawMarkdown: true
tocType: flat
comment: true
translations: ['en']
---

主题内置了 **[Giscus](https://giscus.app/zh-CN)**（推荐）与 **[Gitalk](https://github.com/gitalk/gitalk)** 两种评论系统，均采用按需懒加载机制（滚动接近评论区时才加载脚本资源）。

> 通用说明：
> - 评论区语言会自动跟随文章的 `language` 或站点 `_config.yml` 中的 `language`，无需单独配置。
> - 如需在单篇文章中关闭评论区，可在文章 Front Matter 中添加 `comment: false`。
> - 如需默认关闭、仅在指定文章按需开启评论区（如本页），可在 `_config.linen.yml` 的 `comment` 下设置 `enable: false`，再在目标文章的 Front Matter 中添加 `comment: true`。
> - 省略 `provider` 时，主题会自动根据字段识别：配置了 `repo_id` / `category_id` 时使用 **Giscus**，配置了 `client_id` 时使用 **Gitalk**。

## Giscus（推荐）

[Giscus](https://giscus.app/zh-CN) 基于 GitHub Discussions，无需在前端暴露 `client_secret`，体积极轻，且内置支持随 Linen 顶部深色/浅色切换按钮实时同步主题配色。

在 `_config.linen.yml` 中加入以下配置：

```yaml _config.linen.yml
comment:
  provider: giscus                 # 可选，存在 repo_id / category_id 时会自动识别
  repo: owner/repo                 # GitHub 仓库（需开启 Discussions）
  repo_id: R_kgDO...               # 仓库 ID
  category: Announcements          # Discussion 分类名（可选）
  category_id: DIC_kwDO...         # 分类 ID
  mapping: pathname                # 可选，默认 pathname
  strict: "0"                      # 可选，默认 "0"
  reactions_enabled: "1"           # 可选，默认 "1"
  emit_metadata: "0"               # 可选，默认 "0"
  input_position: top              # 可选，默认 top（top | bottom）
  light_theme: linen               # 可选，浅色模式下的 Giscus 主题，默认 linen（内置主题，支持自定义 CSS URL 或官方主题名）
  dark_theme: linen                # 可选，深色模式下的 Giscus 主题，默认 linen（本地 HTTP 预览时会自动回退到 light / dark_dimmed）
  # theme: light                   # 可选，若设置固定主题则不再跟随深浅色切换
  # lang: zh-CN                    # 可选，默认跟随页面/站点语言
```

### Giscus 配置步骤

1. 准备一个**公开（Public）**的 GitHub 仓库，并在仓库的 **Settings → Features** 中勾选开启 **Discussions**。
2. 前往 [GitHub Apps - giscus](https://github.com/apps/giscus)，将 giscus 应用安装到该仓库。
3. 打开 [giscus.app/zh-CN](https://giscus.app/zh-CN)，输入仓库名（`owner/repo`）并选择 Discussion 分类，页面会自动生成 `data-repo-id` 与 `data-category-id`。
4. 将生成的 `repo`、`repo_id`、`category`、`category_id` 填入 `_config.linen.yml` 的 `comment` 字段即可。

## Gitalk

如果需要继续使用基于 GitHub Issues 的 Gitalk，在 `_config.linen.yml` 中加入以下配置：

```yaml _config.linen.yml
comment:
  provider: gitalk                 # 可选，默认兼容
  client_id: ****
  client_secret: ***
  repo: ***
  owner: ***
  admin:
    - ***
  pager_direction: last            # 可选，默认 last（最新评论在前）
  proxy: https://your-proxy.example.com/?url=https://github.com/login/oauth/access_token # 可选，建议替换为自建代理地址
```

### Gitalk 配置指南

> 以下内容引用自 [Icarus用户指南 - 用户评论插件](https://ppoffice.github.io/hexo-theme-icarus/Plugins/Comment/icarus%E7%94%A8%E6%88%B7%E6%8C%87%E5%8D%97-%E7%94%A8%E6%88%B7%E8%AF%84%E8%AE%BA%E6%8F%92%E4%BB%B6/#Gitalk)

1. 登录GitHub并[点此注册](https://github.com/settings/applications/new)一个新的OAuth应用。
   填写“应用名称”(Application name)，“应用主页”(Homepage URL)，“应用描述”(Application description)。
   然后，在“认证回调地址”(Authorization callback URL)填写你的博客的根URL地址。
   点击“注册应用”(Register application)按钮来跳转到应用详情界面。

    <img style="max-width: 500px;" alt="注册OAuth应用 - GitHub" src="/hexo-theme-linen-doc-zh-CN/img/gitalk-register-application.jpg">

2. 复制“Client ID”与“Client Secret”的值并填入主题配置的相应配置项中。
    <img style="max-width: 500px;" alt="OAuth应用设置 - GitHub" src="/hexo-theme-linen-doc-zh-CN/img/gitalk-application-settings.jpg">

   例如，对于下面的“Client ID”和“Client Secret”：

    ```text GitHub OAuth应用
    Client ID
    xxxxxxxxxxxxxxxxxxxx
    Client Secret
    xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    ```

   对应如下的 Gitalk 的配置：

    ```yaml _config.linen.yml
    comment:
      client_id: xxxxxxxxxxxxxxxxxxxx
      client_secret: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
      repo: Some-of-Your-GitHub-Repo
      owner: your_github_name
      admin:
        - your_github_name
      pager_direction: last           # 可选填，默认 last
      proxy:                          # 可选填，CORS 代理地址
    ```

3. 关于上述配置的含义和可选值，请参考 [Gitalk文档](https://github.com/gitalk/gitalk)。
